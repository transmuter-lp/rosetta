# Rosetta
General purpose text and binary files mapping tool.

Based on [Source Map](https://tc39.es/source-map/).

## Features

- Better suited for mapping between medium/large multi-file projects:
    - Centralized file indexes.
    - Individual mappings file for each source file.
    - Mappings overlays.
- More focus in being human-friendly than machine-friendly.
- Hash-based tracking of mapped files to detect out-of-sync mappings.
- Supports mapping files in text or binary format.
- Maps ranges:
    - More accurate and semantic.
    - Can nest and overlap.

## Specification

### Terminology

- **Source file**: A file that is being mapped from.
- **Destination file**: A file that is being mapped to.
- **Mappings overlay**: A named grouping of mappings files that can be overlayed hierarchically. The base overlay is anonymous.
- **Sources index**: A `sources{.<overlay-name>}.rosetta` file that lists source files and their formats.
- **Destinations index**: A `destinations{.<overlay-name>}.rosetta` file that lists destination files and their formats.
- **Mappings file**: A `<source-file>{.<overlay-name>}.rosetta` file that maps one source file to one or more destination files.
- **Source root path**: The filesystem path under which all source files are stored.
- **Destination root path**: The filesystem path under which all destination files are stored.
- **Mappings root path**: The filesystem path under which the index files and all mappings files are stored. The mappings files must be stored in the same relative paths of their source files.

### Mapping format

The index files are broken down as follows:

- Each file entry is separated by a semicolon (`;`).
- Each file entry is made up of 3 fields.
- Each field is separated by a comma (`,`).

The fields in each file entry are:

1. `file_path`: The path of the file, relative to the root path.
2. `file_format`: The format of the file, can be either `t` for text or `b` for binary.
3. `file_hash`: The SHA-256 hash of the file.

The mappings file is broken down as follows:

- Each range is separated by a semicolon (`;`).
- Each range is made up of 5, 7 or 9 fields.
- Each field is separated by a comma (`,`).

The fields in each range are:

1. `source_start_column_offset`: The starting one-based column (in text format) or zero-based offset (in binary format) in the source file.
2. `source_end_column_offset`: The ending one-based column (in text format) or zero-based offset (in binary format) in the source file.
3. `destination`: The zero-based index of the destination file entry into the destinations index. The index of file entries continue from the previous overlay.
4. `destination_start_column_offset`: The starting one-based column (in text format) or zero-based offset (in binary format) in the destination file.
5. `destination_end_column_offset`: The ending one-based column (in text format) or zero-based offset (in binary format) in the destination file.
6. `source_start_line`: The starting one-based line in the source file. *This field is not present when the source file is in binary format*.
7. `source_end_line`: The ending one-based line in the source file. *This field is not present when the source file is in binary format*.
8. `destination_start_line`: The starting one-based line in the destination file. *This field is not present when the destination file is in binary format*.
9. `destination_end_line`: The ending one-based line in the destination file. *This field is not present when the destination file is in binary format*.
