#!/bin/bash

# Function to unpack a single file
unpack_file() {
  local file="$1"
  local result

  case $(file -b "$file" | awk '{print $1}') in
    gzip | compress)
      gzip -d -q -f "$file" ;;
    bzip2)
      bunzip2 -q -f "$file" ;;
    Zip)
      unzip -q -o "$file" ;;
    *)
      return 1 ;; # failure
  esac

  result=$?
  [ "$verbose" = true ] && echo "$([ $result -eq 0 ] && echo 'Unpacked' || echo 'Failed to unpack') $file..."
  return $result
}

# Function to recursively unpack files in a directory
unpack_directory() {
  local directory="$1"
  local archives_decompressed=0
  local files_not_decompressed=0

  for file in "$directory"/*; do
    if [ -d "$file" ]; then
      unpack_directory "$file"
    elif unpack_file "$file"; then
      ((archives_decompressed++))
    else
      ((files_not_decompressed++))
    fi
  done

  ((archives_decompressed_total+=archives_decompressed))
  ((files_not_decompressed_total+=files_not_decompressed))
}

# Display the script's manual
print_manual() {
  echo "Usage: $0 [-r] [-v] file1 [file2 ...]"
  echo "Unpacks compressed files."
  echo
  echo "Options:"
  echo "  -r    Recursively unpack files in directories."
  echo "  -v    Verbose mode. Print additional information."
  echo
  echo "Arguments:"
  echo "  file1, file2, ...    The file(s) to unpack."
  echo
  echo "Note: Supported compressed file formats are gzip, compress, bzip2, and Zip."
}

# Main script logic
recursive=false
verbose=false
archives_decompressed_total=0
files_not_decompressed_total=0

# Parse command-line options
while getopts "rv" opt; do
  case $opt in
    r) recursive=true ;;
    v) verbose=true ;;
    *) print_manual; exit 1 ;;
  esac
done

shift $((OPTIND - 1))

# Ensure at least one file is provided
if [ $# -eq 0 ]; then
  echo "Error: No file(s) provided."
  print_manual
  exit 1
fi

# Process each file or directory
for file in "$@"; do
  if [ -d "$file" ] && [ "$recursive" = true ]; then
    unpack_directory "$file"
  elif unpack_file "$file"; then
    ((archives_decompressed_total++))
  else
    ((files_not_decompressed_total++))
  fi
done

# Display results
echo "Decompressed $archives_decompressed_total archive(s)"
exit $files_not_decompressed_total
