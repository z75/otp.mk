otp.mk
======

Tiny Makefile-based Erlang/OTP and reltool/relx/rebar/mix compatible build solution.

Overview
--------

Everyone preffer its own Erlang build solution along with its favourite Erlang language.
We want to introduce our vision for maintaining Erlang projects. Doesn't matter you use
pure OTP reltool or rebar/relx or even Elixir mix we whant to hide implementation of those
tools behind makefile otp.mk.

Architecture
============

Resolving Dependencies
----------------------

There are severals way to do so: using rebar.config, using mix.exs or using information
based on *.app.src files. Basic resolving neeeded for determinig correct order of
application:start(App) for launching release in developer mode.
We are using reltool_server for that purposes in depman.erl.

    rebar
    mix
    reltool

Releasing
---------

We support all ways of releasing, but for keeping simple we have chosen relx by Eric Merritt.
In case you are using raw "rebar -f generate" or "relx" releasing in development mode you should
substitute all ebin folder with symlinks to appropriate ebin in apps/deps folder to make Rusty's sync work.
relx.config is generating based on APPS RELEASE NODE COOKIE information.

    relx
    rebar -f generate
    reltool

Building
--------

Each Erlang language use its own compiler, so for Elixir we need to use mix,
for Joxa we need to use joxa and for Erlang we can use rebar or raw erlc. Knowing the build
order we can use raw erlc using reltool tree.

    mix
    joxa
    rebar
    erlc

Variables
---------

    APPS        -- n2o n2o_sample cowboy erlydtl ranch gproc mimetypes
    RELEASE     -- unirel
    NODE        -- node@localhost
    COOKIE      -- secret
    ERL_ARGS    -- -args_file vm.args -config sys.config
    RUN_DIR     -- .
    LOG_DIR     -- logs
    ROOTS       -- apps deps

Prerequisites in PATH
---------------------

    joxa
    elixir
    erlc
    mix
    rebar
    make
    relx
    to_erl
    run_erl

Commands
--------

    make get-deps		Get-Deps from rebar.config
    make update-deps	Update-Deps from rebar.config
    make [compile]		Compile Dependencies with rebar
    make .applist		Generate Applications List
    make clean			Clean BEAM Files
    make console		Run Apps in Dev Mode Console
    make start			Start bundle with run_erl in Dev Mode
    make attach			Attach to bundle with to_erl in Dev Mode
    make release		Build Release with relx
    make dialyzer		Run OTP Dializer
    make tar			Pack relx relase without ERTS
    make ct				Run Common Test suite
    make eunit			Run eunit

See real example of usage in https://github.com/5HT/skyline

TODO
----

1. mix support
2. rebar.config compatible rebar replacement

Credits
-------

* Vladimir Kirillov
* Maxim Sokhatsky
* Max Treskin

OM A HUM
