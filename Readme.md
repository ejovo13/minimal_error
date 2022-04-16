# What's wrong?

When trying to factor out common behavior for a simple Matrix library, I ran into a strange problem.
In `Minimal.hpp` there are 3 classes. `Grid1D`, an abstract base class; `Grid2D`, an abstract class that
is derived from `Grid1D`; and a final concrete class `Matrix` that is derived from `Grid2D`.
`Grid1D -> Grid2D -> Matrix`.

I have two versions of indexing functions, one version that takes 1 parameter `at(int i)` and `operator()(int i)` which are defined by `Grid1D` and another version taking two coordinates, `at(int i, int j)` and `operator()(int i, int j)` defined in `Grid2D`.

Here's what's going wrong: `Grid2D`'s implementation of `at` overshadows `Grid1D`'s implementation. I would like to have these different modes of accessing data separated into these two separate ABCs, while still having the luxury of indexing a matrix either by a single vector coordinate or by row and col indices.

# What do I want to know?

Why is `at(int i)` invisible to `Matrix`?