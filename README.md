This is a CMake wrapper for fast-csv-parser (https://github.com/ben-strasser/fast-cpp-csv-parser)

## Usage
Make this repository a submodule of your project. Then add in your CMakeLists.txt:

```
# add the path to this project
add_subdirectory(strasser)

# ...

target_link_libraries(your-target PUBLIC strasser::csv_parser)
```
