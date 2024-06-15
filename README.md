# OTP Build Script

A script to build Erlang/OTP with embedded, statically linked OpenSSL crypto, a suitable Rebar
version, optional documentation, and optional graphical tools.

## Usage

Invoke `otp-build -h` for command line requirements and options.

## Why?

I wrote it because I wanted more control over what was built.

I'm publishing it because a couple of people have expressed interest.

Use it if you like it, or don't.

## Supported OTP Releases

Theoretically, this _should_ be able to build releases from `R15` onward.
In practice, I don't have any suitable build environments set up that can build that far back.

In particular, the OpenSSL version required prior to OTP-17 only builds on `x86`, and I do just
about everything on `arm64` Macs these days.

Some day I'll probably dust off an `x86_64` machine and give the older versions a spin, but that's
a pretty low priority.

## Why Not Kerl?

[kerl][Kerl] _was_ around when I started tinkering with the ancestors of this script, and I did use
it enough times to determine I wanted better control over the build process, particularly on Macs
where I was doing my primary building at that time.

The `activate` model was inspired by similar behavior in `kerl_activate` but is not meant to be
compatible ... though it _could_ be made so with little effort.

## Origin

Sometime in the middle of 2014 I started gathering together the assorted scripts and commands I'd
been using to build Erlang/OTP for experimentation into a marginally neater collection.
Some of that eventually went into scripts in the [local_env][LocalEnv] repo, and serves as the
basis of the primary script here.

## License

To the extent anyone cares, consider it all covered by this highly permisive [license][License].

  [Kerl]:       https://github.com/kerl/kerl
  [LocalEnv]:   https://github.com/tburghat/local_env
  [OTP]:        https://github.com/erlang/otp
  [License]:    LICENSE
