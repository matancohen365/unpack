
# File Unpacking Script

This repository contains a Bash script for unpacking compressed files. The script provides the functionality to decompress files of various compression types, including gzip, bzip2, zip, and compress.

## Usage

You can use this script to efficiently unpack compressed files in a directory.

### Prerequisites

- Bash shell (Most Unix-like systems come with Bash pre-installed)
- `file` command for determining compression type
- `gunzip`, `bunzip2`, `unzip`, and `uncompress` commands for decompression (Make sure these are available on your system)

### Running the Script

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/your-username/file-unpacking-script.git
   ```

2. Change into the repository directory:

   ```bash
   cd file-unpacking-script
   ```

3. Make the script executable:

   ```bash
   chmod +x unpack.sh
   ```

4. Run the script with desired options and file paths:

   ```bash
   ./unpack.sh [options] file1 file2 directory1 ...
   ```

   Available options:
   
   - `-r`: Enable recursive unpacking for directories (optional)
   - `-v`: Enable verbose output (optional)

   Example usage:

   ```bash
   ./unpack.sh -r -v compressed_directory/file1.gz compressed_file.zip another_directory
   ```

### Example

Suppose you have a directory named `archives` containing compressed files, and you want to unpack them:

```bash
./unpack.sh -r archives
```

This command will recursively unpack all files in the `archives` directory.

## Contributions

Contributions to this repository are welcome! Feel free to submit issues and pull requests.

## License

This project is licensed under the [MIT License](LICENSE).