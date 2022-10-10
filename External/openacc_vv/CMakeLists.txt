# OPENACC Validation & Verification Suite
# https://crpl.cis.udel.edu/oaccvv/
cmake_minimum_required (VERSION 3.16.3)
include(External)

option(TEST_SUITE_OPENACCVV_FORCE_ALL "Execute all OPENACC V&V tests, even those known to be unsupported by Clang" OFF)
set(OpenACC_C_FLAGS "-fopenacc -fopenmp-targets=nvptx64-nvidia-cuda -lm" CACHE INTERNAL "OpenACC C flags")
set(OpenACC_CXX_FLAGS "-fopenacc -fopenmp-targets=nvptx64-nvidia-cuda -lm" CACHE INTERNAL "OpenACC CXX flags")

set(TEST_SUITE_EXTERNALS_DIR "" CACHE PATH
    "Directory containing test-suite external benchmark sources")

set(TEST_SUITE_OPENACCVV_EXPECT_PASS
 acc_copyin.c
 acc_copyout.c
 acc_copyout_finalize.c
 acc_create.c
 acc_delete.c
 acc_delete_finalize.c
 acc_get_device_num.c
 acc_get_device_type.c
 acc_get_num_devices.c
 acc_hostptr.c
 acc_is_present.c
 acc_map_data.c
 acc_memcpy_device.c
 acc_on_device.c
 acc_set_device_num.c
 acc_set_device_type.c
 acc_unmap_data.c
 acc_update_device.c
 acc_update_self.c
 atomic_bitand_equals.c
 atomic_bitor_equals.c
 atomic_bitxor_equals.c
 atomic_capture_bitand_equals.c
 atomic_capture_bitor_equals.c
 atomic_capture_bitxor_equals.c
 atomic_capture_divided_equals.c
 atomic_capture_expr_bitand_x.c
 atomic_capture_expr_bitor_x.c
 atomic_capture_expr_bitxor_x.c
 atomic_capture_expr_divided_x.c
 atomic_capture_expr_lshift_x.c
 atomic_capture_expr_minus_x.c
 atomic_capture_expr_multiply_x.c
 atomic_capture_expr_plus_x.c
 atomic_capture_expr_rshift_x.c
 atomic_capture_lshift_equals.c
 atomic_capture_minus_equals.c
 atomic_capture_multiply_equals.c
 atomic_capture_plus_equals.c
 atomic_capture_postdecrement.c
 atomic_capture_postincrement.c
 atomic_capture_predecrement.c
 atomic_capture_preincrement.c
 atomic_capture_rshift_equals.c
 atomic_divided_equals.c
 atomic_expr_bitand_x.c
 atomic_expr_bitor_x.c
 atomic_expr_bitxor_x.c
 atomic_expr_divided_x.c
 atomic_expr_lshift_x.c
 atomic_expr_minus_x.c
 atomic_expr_multiply_x.c
 atomic_expr_plus_x.c
 atomic_expr_rshift_x.c
 atomic_lshift_equals.c
 atomic_minus_equals.c
 atomic_multiply_equals.c
 atomic_plus_equals.c
 atomic_postdecrement.c
 atomic_postincrement.c
 atomic_predecrement.c
 atomic_preincrement.c
 atomic_rshift_equals.c
 atomic_structured_assign_assign.c
 atomic_structured_assign_bitand_equals.c
 atomic_structured_assign_bitor_equals.c
 atomic_structured_assign_bitxor_equals.c
 atomic_structured_assign_divided_equals.c
 atomic_structured_assign_expr_bitand_x.c
 atomic_structured_assign_expr_bitor_x.c
 atomic_structured_assign_expr_bitxor_x.c
 atomic_structured_assign_expr_divided_x.c
 atomic_structured_assign_expr_multiply_x.c
 atomic_structured_assign_expr_plus_x.c
 atomic_structured_assign_lshift_equals.c
 atomic_structured_assign_minus_equals.c
 atomic_structured_assign_multiply_equals.c
 atomic_structured_assign_plus_equals.c
 atomic_structured_assign_postdecrement.c
 atomic_structured_assign_postincrement.c
 atomic_structured_assign_predecrement.c
 atomic_structured_assign_preincrement.c
 atomic_structured_assign_rshift_equals.c
 atomic_structured_assign_x_bitand_expr.c
 atomic_structured_assign_x_bitor_expr.c
 atomic_structured_assign_x_bitxor_expr.c
 atomic_structured_assign_x_divided_expr.c
 atomic_structured_assign_x_lshift_expr.c
 atomic_structured_assign_x_minus_expr.c
 atomic_structured_assign_x_multiply_expr.c
 atomic_structured_assign_x_plus_expr.c
 atomic_structured_assign_x_rshift_expr.c
 atomic_structured_bitand_equals_assign.c
 atomic_structured_bitor_equals_assign.c
 atomic_structured_bitxor_equals_assign.c
 atomic_structured_divided_equals_assign.c
 atomic_structured_expr_bitand_x_assign.c
 atomic_structured_expr_bitor_x_assign.c
 atomic_structured_expr_bitxor_x_assign.c
 atomic_structured_expr_multiply_x_assign.c
 atomic_structured_expr_plus_x_assign.c
 atomic_structured_lshift_equals_assign.c
 atomic_structured_minus_equals_assign.c
 atomic_structured_multiply_equals_assign.c
 atomic_structured_plus_equals_assign.c
 atomic_structured_postdecrement_assign.c
 atomic_structured_postincrement_assign.c
 atomic_structured_predecrement_assign.c
 atomic_structured_preincrement_assign.c
 atomic_structured_rshift_equals_assign.c
 atomic_structured_x_bitand_expr_assign.c
 atomic_structured_x_bitor_expr_assign.c
 atomic_structured_x_bitxor_expr_assign.c
 atomic_structured_x_divided_expr_assign.c
 atomic_structured_x_lshift_expr_assign.c
 atomic_structured_x_minus_expr_assign.c
 atomic_structured_x_multiply_expr_assign.c
 atomic_structured_x_plus_expr_assign.c
 atomic_structured_x_rshift_expr_assign.c
 atomic_update_bitand_equals.c
 atomic_update_bitor_equals.c
 atomic_update_bitxor_equals.c
 atomic_update_divided_equals.c
 atomic_update_expr_bitand_x.c
 atomic_update_expr_bitor_x.c
 atomic_update_expr_bitxor_x.c
 atomic_update_expr_divided_x.c
 atomic_update_expr_lshift_x.c
 atomic_update_expr_minus_x.c
 atomic_update_expr_multiply_x.c
 atomic_update_expr_plus_x.c
 atomic_update_expr_rshift_x.c
 atomic_update_lshift_equals.c
 atomic_update_minus_equals.c
 atomic_update_multiply_equals.c
 atomic_update_plus_equals.c
 atomic_update_postdecrement.c
 atomic_update_postincrement.c
 atomic_update_predecrement.c
 atomic_update_preincrement.c
 atomic_update_rshift_equals.c
 atomic_update_x_bitand_expr.c
 atomic_update_x_bitor_expr.c
 atomic_update_x_bitxor_expr.c
 atomic_update_x_divided_expr.c
 atomic_update_x_lshift_expr.c
 atomic_update_x_minus_expr.c
 atomic_update_x_multiply_expr.c
 atomic_update_x_plus_expr.c
 atomic_update_x_rshift_expr.c
 atomic_x_bitand_expr.c
 atomic_x_bitor_expr.c
 atomic_x_bitxor_expr.c
 atomic_x_divided_expr.c
 atomic_x_lshift_expr.c
 atomic_x_minus_expr.c
 atomic_x_multiply_expr.c
 atomic_x_plus_expr.c
 atomic_x_rshift_expr.c
 data_copy_no_lower_bound.c
 data_copyin_no_lower_bound.c
 data_copyout_no_lower_bound.c
 data_copyout_reference_counts.c
 data_create.c
 data_create_no_lower_bound.c
 data_present_no_lower_bound.c
 data_with_changing_subscript.c
 data_with_structs.c
 enter_data_copyin_no_lower_bound.c
 enter_data_create.c
 enter_data_create_no_lower_bound.c
 exit_data.c
 exit_data_copyout_no_lower_bound.c
 exit_data_copyout_reference_counts.c
 exit_data_delete_no_lower_bound.c
 loop_collapse.c
 loop_no_collapse_default.c
 parallel.c
 parallel_copy.c
 parallel_copyin.c
 parallel_copyout.c
 parallel_create.c
 parallel_default_copy.c
 parallel_default_present.c
 parallel_independent_atomic.c
 parallel_independent_atomic_capture.c
 parallel_independent_atomic_read.c
 parallel_independent_atomic_update.c
 parallel_independent_atomic_write.c
 parallel_loop.c
 parallel_loop_gang.c
 parallel_loop_independent.c
 parallel_loop_independent_reduction.c
 parallel_loop_reduction_add_general_type_check_pt1.c
 parallel_loop_reduction_or_loop.c
 parallel_loop_reduction_or_vector_loop.c
 parallel_loop_seq.c
 parallel_loop_tile.c
 parallel_loop_vector.c
 parallel_loop_vector_blocking.c
 parallel_loop_worker.c
 parallel_loop_worker_blocking.c
 parallel_present.c
 parallel_reduction.c
 parallel_scalar_default_firstprivate.c
 parallel_switch.c
 parallel_wait.c
 parallel_wait_devnum.c
 parallel_while_loop.c
)

function (add_openaccvv LANG)
  if ("${LANG}" STREQUAL "C")
    set(_langext ".c")
  elseif ("${LANG}" STREQUAL "CXX")
    set(_langext ".cpp")
  else ()
    message(FATAL_ERROR "Unsupported languge ${LANG}")
  endif ()

  file(GLOB_RECURSE _tests_sources RELATIVE "${TEST_SUITE_OPENACCVV_ROOT}/Tests" "${TEST_SUITE_OPENACCVV_ROOT}/Tests/*${_langext}" )
  foreach (_file IN LISTS _tests_sources)

    if (NOT TEST_SUITE_OPENACCVV_FORCE_ALL AND NOT "${_file}" IN_LIST TEST_SUITE_OPENACCVV_EXPECT_PASS)
            message(STATUS "Skipping OPENACC V&V test ${_file}")
      continue ()
    endif ()

    llvm_test_run()
    llvm_test_executable(${_file} "${TEST_SUITE_OPENACCVV_ROOT}/Tests/${_file}")
    # To specify libraries or flags to use when linking a given target and/or its dependents
    target_link_libraries(${_file} PUBLIC OpenACC::OpenACC_${_lang})
  endforeach ()
endfunction ()


llvm_externals_find(TEST_SUITE_OPENACCVV_ROOT "openacc_vv" "OpenACC Validation & Verification Suite")
if (TEST_SUITE_OPENACCVV_ROOT AND NOT TEST_SUITE_BENCHMARKING_ONLY)
#compiler supports OpenACC, the flags required to compile with OpenACC support are returned in variables for the different languages
find_package(OpenACC REQUIRED)
foreach (_lang in C CXX)
  if (CMAKE_${_lang}_COMPILER)
      add_openaccvv(${_lang})
    endif()
  endforeach ()
endif ()
