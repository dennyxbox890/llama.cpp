# dependencies
#enable O3 flag
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wno-unused-variable -Wno-unused-function -Wno-error")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-Ofast")

#add lto
set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)
find_package(Threads REQUIRED)

# third-party

# ...

# flags

llama_add_compile_flags()

# examples

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if (EMSCRIPTEN)
else()
    add_subdirectory(batched-bench)
    add_subdirectory(batched)
    add_subdirectory(embedding)
    add_subdirectory(eval-callback)

    if (NOT WIN32)
        # disabled on Windows because it uses internal functions not exported with LLAMA_API
        add_subdirectory(gbnf-validator)
    endif()

    add_subdirectory(gguf-hash)
    add_subdirectory(gguf-split)
    add_subdirectory(gguf)
    add_subdirectory(gritlm)
    add_subdirectory(imatrix)
    add_subdirectory(infill)
    add_subdirectory(llama-bench)
    add_subdirectory(lookahead)
    add_subdirectory(lookup)
    add_subdirectory(main)
    add_subdirectory(parallel)
    add_subdirectory(passkey)
    add_subdirectory(perplexity)
    add_subdirectory(quantize)
    add_subdirectory(retrieval)
    if (LLAMA_BUILD_SERVER)
        add_subdirectory(server)
    endif()
    add_subdirectory(save-load-state)
    add_subdirectory(run)
    add_subdirectory(simple)
    add_subdirectory(simple-chat)
    add_subdirectory(speculative)
    add_subdirectory(speculative-simple)
    add_subdirectory(tokenize)
    add_subdirectory(tts)
    add_subdirectory(gen-docs)
    if (NOT GGML_BACKEND_DL)
        # these examples use the backends directly and cannot be built with dynamic loading
        add_subdirectory(convert-llama2c-to-ggml)
        add_subdirectory(cvector-generator)
        add_subdirectory(export-lora)
        if (NOT WIN32)
            # disabled on Windows because it uses internal functions not exported with LLAMA_API
            add_subdirectory(quantize-stats)
        endif()
        add_subdirectory(llava)
        if (GGML_RPC)
            add_subdirectory(rpc)
        endif()
        if (GGML_SYCL)
            add_subdirectory(sycl)
        endif()
    endif()
endif()
