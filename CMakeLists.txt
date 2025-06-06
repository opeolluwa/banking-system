cmake_minimum_required(VERSION 3.31)

project(apex_banking_system)

add_executable(${PROJECT_NAME} main.c
        include/uuidv4.c
        lib/utils.c
        lib/transaction.c
        lib/bank.c
        lib/accounts.c
        include/libbcrypt/bcrypt.c
        include/libbcrypt/crypt_blowfish/crypt_gensalt.c
        include/libbcrypt/crypt_blowfish/crypt_blowfish.c
        include/libbcrypt/crypt_blowfish/wrapper.c

)

include_directories(include lib)

set(CMAKE_C_STANDARD 11)

find_package(SQLite3 3.39 REQUIRED)


#target_link_libraries(${PROJECT_NAME} SQLite3)
##
### Checks if OSX and links appropriate frameworks (only required on MacOS)
##if (APPLE)
##    target_link_libraries(${PROJECT_NAME} "-framework IOKit")
##    target_link_libraries(${PROJECT_NAME} "-framework Cocoa")
##    target_link_libraries(${PROJECT_NAME} "-framework OpenGL")
##endif()


find_library(SQLITE3_LIB sqlite3)
if (NOT SQLITE3_LIB)
    message(FATAL_ERROR "SQLite3 library not found")
endif()

target_link_libraries(${PROJECT_NAME} ${SQLITE3_LIB})