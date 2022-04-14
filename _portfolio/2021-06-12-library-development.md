---
collection: portfolio
title: "Library Development"
excerpt: "A collection of libraries to be used in a game engine<br/><img src='/images/library-development-thumbnail.PNG'>"
---

These libraries are were developed with the goal of encapsulating core functionality needed within a game engine. And, as such, each has been statically linked to a work-in-progress (7/21) game engine application, which also uses GLFW, a graphics library for OpenGL.

## Memory Library

### Library features:

- Memory leak tracking
- Per heap allocations
- Normal heaps
- Fixed block heaps
- Manual alignment requests
- x86/x64 support

The memory library has numerous features for quality-of-life, including memory leak tracking and per heap allocations. The memory leak tracking in this library can give the exact line where the memory that leaked was allocated. The library also supports the ability to add secondary overflow heaps, if the user would like a back-up heap for any overflow allocation requests.



## Math Library

### Library features:

- 3D/4D Vectors
- 4x4 Matrices
- Quaternions
- Optimized for speed using SIMD
- Const & non-const interface
- Vector Linear Interpolation (LERP)
- Quaternion Spherical Linear Interpolation (SLERP)
- x86/x64 support

Every game engine needs a fast and accurate math library. This library is optimized to use SIMD operations, where possible, and verified for accuracy with unit tests. The library is const correct in order to ensure no collision with any user frameworks or coding styles.

The library supports conversions between rotation-only Matrices and Quaternions.

Using setters/getters and nameless unions, each vector and quaternion can be accessed similar to arrays or by function call. This allows the user to access each float individually, but allows the library to use `__m128` for use with SIMD operations.

The library contains an application layer which contains interpolation functions for individual or arrays of vectors and quaternions.


## PCS Tree Library

### Library features:

- Component-Based design pattern
- Object-Oriented implimentation
- Forward/Reverse iterators
- x86/x64 support

The PCS Tree structure is a component-based system which can be thought of as a three-dimensional linked list. Each node contains parent, sibling, and child pointers. This allows for vertical and horizontal traversal. The library is object-oriented rather than templated, allowing for O(1) removal of any PCSNode.

The library contains iterator classes for forward and reverse linear iteration. These non-recursive iterators are friendly towards the stack. The iterators traverse the PCS tree in a forward/reverse depth-first fashion.

## File Library

### Library features:

- Familiar API (similar to C's stdio)
- Scoped enums for easier parameter filling
- Native Windows under the hood for speed
- Directory iterator
- x86 support

This library is a faster implementation of the C stdio library, due to the use of the native Win32 API. It also has a more user-friendly interface than Win32. Using scoped enums, use of the API is much more explicit, where, for instance, to open a file in read only mode, one can simply use `Mode::READ`. This library contains other familiar functions like `Seek()` and `Tell()`.



## Manager Library

### Library features:

- Object-Oriented implementation
- Manager/Pooled Managers
- Tracking stats
- x86/x64 support

One of the simplest and most versitile data containers is the linked list. This library is an object-oriented doubly linked list manager library. Once a class is derived from the base DLink class, it can then be added easily added to a linked list.

The library contains two base manager classes that can be derived from: DLinkManager and BaseManager. The BaseManager is to be used for any objects you would like to pool in order to reduce memory allocation/deallocations. Both manager classes contain stat tracking, such as nodes currently on list and max nodes on list. The Pooled Manager also contains information about the number of nodes created, the numbers of nodes active, and the number of nodes on the reserve list.

By using the object-oriented approach, as opposed to templates, each object can be removed from the list in O(1), as long as you have a reference to the object.
