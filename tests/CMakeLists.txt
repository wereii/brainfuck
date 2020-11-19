cmake_minimum_required(VERSION 3.10)

# add_compile_run_test(test_name source_file)
function(add_compile_run_test)
    if (NOT ${ARGC} MATCHES 2)
        message(FATAL_ERROR "add_compile_run_test; Missing arguments")
    endif ()

    set(TEST_NAME "${ARGV0}")
    set(TEST_NAME_COMP "${TEST_NAME}_compile")
    set(TEST_NAME_CLEAN "${TEST_NAME}_cleanup")

    set(SRC_FILE "${ARGV1}")
    set(OUT_FILE "${SRC_FILE}.out")

    # Compile
    add_test(NAME "${TEST_NAME_COMP}" COMMAND bfcc ${SRC_FILE} -o ${OUT_FILE}
            WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/tests)
    set_tests_properties("${TEST_NAME_COMP}" PROPERTIES FIXTURES_SETUP COMP)

    # Run
    add_test(NAME "${TEST_NAME}" COMMAND ./${OUT_FILE}
            WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/tests)
    set_tests_properties("${TEST_NAME}" PROPERTIES DEPENDS "${TEST_NAME_COMP}")
    set_tests_properties("${TEST_NAME}" PROPERTIES FIXTURES_REQUIRED COMP)

    # Cleanup
    add_test(NAME "${TEST_NAME_CLEAN}" COMMAND rm -f ./${OUT_FILE}
            WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/tests)
    set_tests_properties("${TEST_NAME_CLEAN}" PROPERTIES DEPENDS "${TEST_NAME_COMP}")
    set_tests_properties("${TEST_NAME_CLEAN}" PROPERTIES FIXTURES_CLEANUP COMP)
endfunction()

add_compile_run_test(hello_world hello_world.bf)
set_tests_properties(hello_world PROPERTIES PASS_REGULAR_EXPRESSION "^Hello World!\n?$")

# add_compile_run_test(comment comment.bf)
# set_tests_properties(comment PROPERTIES PASS_REGULAR_EXPRESSION "^A\n?$")
