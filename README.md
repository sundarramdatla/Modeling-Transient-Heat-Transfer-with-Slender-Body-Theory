# Slender Body Theory

Originating from the study of Stokes flow, Slendery Body Theory can be applied to heat transfer problems where the source geometry is sufficiently longer than its radius and its radius is sufficiently smaller than the diffusion length of the heat. 
The body is parameterized to its centerline, which is discretized into 'pipe elements' of some appropriate element length such that the geometry is respected. The body is assumed to be in an infinite conductive medium whose thermal properties do not depend on the temperature. 
An inner solution of temperature approximates the geometry seen by a point close to the body as an infinite cylindrical source, while farfield points will 'see' a series of discrete point sources, which can be realized as an 'outer solution' by convoluting the heat kernel with the heat point sources.
By matching the limits of the inner and outer temperature solutions, the final temperature solution is achieved and once discretized becomes a system of linear equations that can be solved for the heat transfer from the body. 

For the benchmark problem of a cylinder at constant temperature 10C in an infinite conductive medium of constant temperature 0C, heat transfer is solved for via building the system of linear equations and matrix inversion. The coefficients for the linear system are calculated via a decision tree that takes
nondimensional Fourier numbers as inputs to determine appropriate choice of coefficients, which greatly simplifies computation. For example, if one were to discretize the cylindrical centerline and only consider heat flux from the midpoint, then mesh points on the centerline far from the mid point would contribute less
to the heat flux of the middle, thus their coefficients end up being 0 and they are not relevant for calculating heatflux to the midpoint. This decision tree greatly speeds up computation time by forcing the algorithm to only focus on relevant terms without a loss in accuracy, and allows one to simulate long time scale behavior of temperature distributions.

The cylinder is of length 10m with radius 0.05m and discretized into 10 points. The infinite conductive medium has a thermal conductivity of 1 W/mK and diffusivity of 1x10^-6 m^2/s.
Logarithmic time is used from 10^2 to 10^9 seconds (approximately 31 years) with 150 time steps. Heat flux and time is nondimensionalized by Q/(delta T * k) and sqrt(diffusivity * time) respectively.

Nondimensionalized heat flux versus time data matches that of the results of Koenraad F. Beckers, the author of the seminal paper on studying heat transfer via Slender Body Theory [ref], with root mean square error of 2.848 W and mean absolute error of 0.406.


Ref: https://royalsocietypublishing.org/rspa/article/471/2184/20150494/57825/Slender-body-theory-for-transient-heat-conduction
