# Rosetta
General purpose text and binary files mapping tool.

Based on [Source Map](https://tc39.es/source-map/).

## Features

- Best suited for mapping between entire multi-file projects:
    - Centralized sources/destinations list files.
    - Individual mappings file for each source file.
- More focus in being human-friendly than machine-friendly.
- Hash-based tracking of mapped files to detect out-of-date mappings.
- Supports mapping files in text or binary format.
- Maps ranges:
    - More accurate and semantic.
    - Can nest and overlap.

## Specification

A Rosetta mapping is composed of `sources.rosetta` and `destinations.rosetta` files stored in the sources root path, along with `<filename-with-extension>.rosetta` files for each file listed in `sources.rosetta`, stored in the same path as the source file.

The `sources.rosetta` and `destinations.rosetta` files are broken down as follows:

- Each entry is separated by a semicolon (`;`).
- Each entry is made up of 3 fields.
- Each field is separated by a comma (`,`).

The fields in each entry are:

1. `file_path`: The path of the file, relative to the sources/destinations root path.
2. `file_hash`: The SHA-256 hash of the file.
3. `file_format`: The format of the file, can be either `t` for text or `b` for binary.

The `<filename-with-extension>.rosetta` files are broken down as follows:

- Each range is separated by a semicolon (`;`).
- Each range is made up of 5, 7 or 9 fields.
- Each field is separated by a comma (`,`).

The fields in each range are:

1. `source_start_column`: The starting one-based column (in text format) or zero-based offset (in binary format) in the source file.
2. `source_end_column`: The ending one-based column (in text format) or zero-based offset (in binary format) in the source file.
3. `destination`: The zero-based index of the destination file entry into the `destinations.rosetta` file.
4. `destination_start_column`: The starting one-based column (in text format) or zero-based offset (in binary format) in the destination file.
5. `destination_end_column`: The ending one-based column (in text format) or zero-based offset (in binary format) in the destination file.
6. `source_start_line`: The starting one-based line in the source file. *This field is not present when the source file is in binary format*.
7. `source_end_line`: The ending one-based line in the source file. *This field is not present when the source file is in binary format*.
8. `destination_start_line`: The starting one-based line in the destination file. *This field is not present when the destination file is in binary format*.
9. `destination_end_line`: The ending one-based line in the destination file. *This field is not present when the destination file is in binary format*.
