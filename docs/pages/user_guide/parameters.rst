Parameters
==========

As part of the upgrade from **Incompact3d 2.0** to the now called **Xcompact3d 3.0**, the parameters file was reconfigured to support *NAMELIST I/O*, which produces format-free input for groups of variables. A set of demonstrations of the supported flow configurations are available at :ref:`Benchmark Cases`.

For a complete view about how the `.i3d` files are handled, besides to the default value applied to each parameter when not defined by the user, take a look at `parameters.f90 <https://github.com/xcompact3d/Incompact3d/blob/master/src/parameters.f90>`_\ .

BasicParam
----------

* ``p_row`` & ``p_col`` define the domain decomposition for (large-scale) parallel computation. Notice that the product of both should be equal to the number of computational cores where Xcompact3d will run, and ``p_row = p_col = 0`` executes the code in auto-tuning mode. More information can be found at `2DECOMP&FFT <http://www.2decomp.org>`_\ );

* ``nx``, ``ny`` & ``nz`` are the number of mesh points in each direction;

* ``xlx``, ``yly`` & ``zlz`` are the domain size;

* ``itype`` sets the flow configuration, each one is specified in a different ``BC.<flow-configuration>.f90`` file. They are:

    - 0 - :ref:`User Custom Configuration`;
    - 1 - :ref:`Turbidity Current in Lock-Release`;
    - 2 - :ref:`Taylor-Green Vortices`;
    - 3 - :ref:`Periodic Turbulent Channel`;
    - 4 - :ref:`Periodic Hill`;
    - 5 - :ref:`Flow over a Cylinder`;
    - 6 - Debug Schemes (for developers);
    - 7 - Mixing Layer;
    - 8 - Turbulent Jet;
    - 9 - :ref:`Turbulent Boundary Layer`.

* ``istret`` controls mesh refinement in y:

    - 0 - No refinement (default);
    - 1 - Refinement at the center;
    - 2 - Both sides;
    - 3 - Just near the bottom.

* ``beta`` is the refinement parameter;

* ``iin`` defines perturbation at the initial condition:

    - 0 - No random noise (default);
    - 1 - Random noise with amplitude of ``init_noise``;
    - 2 - Random noise with fixed seed (important for development and debugging) and amplitude of ``init_noise``.

    .. note::
      The exactly behavior may be different according to each flow configuration.

* ``inflow_noise`` Random number amplitude at inflow boundary;

* ``re`` Reynolds number;

* ``dt`` Time step;

* ``ifirst`` First iteration;

* ``ilast`` Last iteration;

* ``numscalar`` Number of scalar fraction, which can have different properties (see :ref:`ScalarParam`);

* ``iscalar`` Enables scalar field(s). It is defined to 1 automatically when ``numscalar > 0``;

* ``iibm`` Flag for Immersed Boundary Method:

    - 0 - Off (default);
    - 1 - On with direct forcing method, i.e., it sets velocity to zero inside the solid body;
    - 2 - On with alternating forcing method, i.e, it uses Lagrangian Interpolators to define the velocity inside the body and imposes no-slip condition at the solid/fluid interface.

* ``ilmn`` Enables Low Mach Number methodology when set to 1;

* ``ilesmod`` Enables Large-Eddy methodologies:

    - 0 - Off;
    - 1 - Smag;
    - 2 - WALE;
    - 3 - dyn Smag;
    - 4 - isVV.

* ``nclx1``, ``nclxn``, ``ncly1``, ``nclyn``, ``nclz1`` & ``nclzn`` define the velocity's boundary condition:

    - 0 - Periodic;
    - 1 - Free-slip;
    - 2 - Dirichlet.

* ``ivisu`` enables store snapshots;

* ``ipost`` enables online postprocessing;

* ``gravx``, ``gravy`` & ``gravz`` are the three components of the unitary vector pointing in the gravity's direction;

NumOptions
----------

* ``ifirstder`` Scheme for first order derivative:

    - 1 - 2nd central;
    - 2 - 4th central;
    - 3 - 4th compact;
    - 4 - 6th compact.

* ``isecondder`` Scheme for second derivative:

    - 1 - 2nd central;
    - 2 - 4th central;
    - 3 - 4th compact;
    - 4 - 6th compact;
    - 5 - hyperviscous 6th.

* ``itimescheme`` Time integration scheme:

    - 1 - Forwards Euler;
    - 2 - Adams-Bashforth 2;
    - 3 - Adams-Bashforth 3;
    - 4 - Adams-Bashforth 4 (not implemented yet);
    - 5 - Runge-kutta 3;
    - 6 - Runge-kutta 4 (not implemented yet);
    - 7 - Semi-implict CN+AB3;
    - 8 - Semi-implict CN+RK3.

* ``nu0nu`` Ratio between hyperviscosity/viscosity at nu;

* ``cnu`` Ratio between hypervisvosity at :math:`k_m=2/3\pi` and :math:`k_c= \pi`.

InOutParam
----------

* ``irestart`` Reads initial flow field if equals to 1;
* ``icheckpoint`` Frequency for writing backup file;
* ``ioutput`` Frequency for visualization;
* ``nvisu`` Size for visual collection;
* ``iprocessing`` Frequency for online postprocessing.

Statistics
----------

* ``spinup_time`` Time after which statistics are collected (in seconds);
* ``nstat`` Size arrays for statistic collection.

ScalarParam
-----------

* ``sc`` Schmidt numbers;
* ``ri`` Richardson numbers;
* ``uset`` Settling velocities;
* ``cp`` Initial concentrations;
* ``nclxS1``, ``nclxSn``, ``nclyS1``, ``nclySn``, ``nclzS1`` & ``nclzSn`` define the scalar's boundary condition:

    - 0 - Periodic;
    - 1 - No-flux;
    - 2 - Dirichlet.

* ``scalar_lbound`` & ``scalar_ubound`` are the Scalar bounds;
* ``iibmS`` Flag for the scalar treatment at the Immersed Boundary Method (pre-release):

    - 0 - Off (default);
    - 1 - On with direct forcing method, i.e., it sets scalar to zero inside the solid body;
    - 2 - On with alternating forcing method, i.e., it uses Lagrangian Interpolators to define the scalar inside the body and imposes zero value at the solid/fluid interface;
    - 3 - On with alternating forcing method, but now the Lagrangian Interpolators are set to impose no-flux for the scalar field at the solid/fluid interface (only recommended if the normal vectors to the object's faces are aligned with one of the coordinate axes).

LESModel
--------

jles, smagcst, walecst, maxdsmagcst, iwall

WallModel
---------

smagwalldamp

Tripping
--------

itrip,A_tr,xs_tr_tbl,ys_tr_tbl,ts_tr_tbl,x0_tr_tbl

ibmstuff
--------

cex,cey,ra,nobjmax,nraf,nvol,iforces

ForceCVs
--------

xld, xrd, yld, yud

LMN
---

dens1, dens2, prandtl, ilmn_bound, ivarcoeff, ilmn_solve_temp, massfrac, mol_weight, imultispecies, primary_species, Fr, ibirman_eos

CASE
----

tgv_twod, pfront
