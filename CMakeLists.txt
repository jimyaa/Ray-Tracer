cmake_minimum_required(VERSION 3.10)
project(RayTracer)
set(CMAKE_CXX_STANDARD 17)

find_package(PNG REQUIRED)

add_executable(RayTracer
    main.cpp
    camera.h
    color.h
    hittable.h
    hittable_list.h
    interval.h
    material.h
    ray.h
    sphere.h
    vec3.h
    wpng.h
)

target_link_libraries(RayTracer PRIVATE PNG::PNG)