# Rosetta
General purpose text and binary files mapping tool.

Based on [Source Map](https://tc39.es/source-map/).

## Features

- Best suited for mapping between entire multi-file projects:
    - Centralized sources/destinations list files.
    - Individual mappings file for each source file.
- More focus in being human-friendly than machine-friendly.
- Supports mapping files in text or binary format.
- Maps ranges:
    - More accurate and semantic.
    - Can nest and overlap.

## Specification

The sources/destinations list files are broken down as follows:

- Each entry is separated by a semicolon (`;`).
- Each entry is made up of 3 fields.
- Each field is separated by a comma (`,`).

The fields in each entry are:

1. `file_path`: The path of the file, relative to the sources/destinations root.
2. `file_hash`: The SHA-256 hash of the file.
3. `file_mode`: The mode of the file, can be either `t` for text or `b` for binary.

The mappings file is broken down as follows:

- Each segment is separated by a semicolon (`;`).
- Each segment is made up of 5, 7 or 9 fields.
- Each field is separated by a comma (`,`).

The fields in each segment are:

1. `source_start_column`: The one-based starting column (in text mode) or offset (in binary mode) in the source file.
2. `source_end_column`: The one-based ending column (in text mode) or offset (in binary mode) in the source file.
3. `destination`: The zero-based index of the destination file entry into the destinations list file.
4. `destination_start_column`: The one-based starting column (in text mode) or offset (in binary mode) in the destination file.
5. `destination_end_column`: The one-based ending column (in text mode) or offset (in binary mode) in the destination file.
6. `source_start_line`: The one-based starting line in the source file. *This field is not present when the source file is in binary mode*.
7. `source_end_line`: The one-based ending line in the source file. *This field is not present when the source file is in binary mode*.
8. `destination_start_line`: The one-based starting line in the destination file. *This field is not present when the destination file is in binary mode*.
9. `destination_end_line`: The one-based ending line in the destination file. *This field is not present when the destination file is in binary mode*.
