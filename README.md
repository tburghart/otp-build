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

## Supported Platforms

OTP releases 25+ _should_ build and run fine with any of the available options, though note that I've as yet to get a build with `wxWidgets` to complete on `FreeBSD`.

Below that things get dicey, particularly with `wxWidgets`, so YMMV.
As you go back to older releases, modern compilers become increasingly cranky about code conformance.
Some of this can probably be addressed by telling compilers to use older code standards, and I've tinkered with that a bit, but it's not a priority for me.
There *MAY* be benefit in using older `autoconf` versions, but I haven't played with that yet.

The OTP `wx` application was rewritten in OTP-24, and I haven't come up with a working version on any platform - working `wx` applications have been produced on various platforms for OTP before and after 24, but none so far on 24 itself.

Below OTP-17, OpenSSL isn't compatible with `arm64` on anything but `Linux`, but these configurations are largely unexplored.

### General Platform Status

| OS | CPU | Status |
|:---|:----|:-------|
| `macOS` | `arm64`  | OTP-21+, some without `wxWidgets` |
| `macOS` | `x64_64` | _as above_ |
| `Linux` | `arm64` | _as above_ |
| `Linux` | `x64_64` | _as above_ |
| `FreeBSD` | `arm64` | OTP-22+ without `wxWidgets` |
| `FreeBSD` | `x64_64` | untested |
| `*BSD` | `*` | untested, _should_ be similar to `FreeBSD` |

### Release & Platform Deets

The following is as much for my own reference as yours.

#### Quirks

| Package | Release | Predicate | What |
|:--------|:--------|:----------|:-----|
| OTP | \< 22 | `FreeBSD` | `configure` can't find required `config.*` files |
| OTP | 19,20 | `macOS >= 10.5` | `configure` broken OS version check |
| OTP | 24 | `macOS` with `wx` | undefined NIF symbols |
| OTP | \< 21 | without `wx` | can't build documentation |
| OpenSSL | 1.0 | `{*BSD,macOS}-arm64` | unsupported configuration |
| wxWidgets | 3.1 | `FreeBSD` | `langinfo.h` doesn't set `_NL_...` macros \* |

> \* The script patches `wxWidgets/src/unix/uilocale.cpp` to not use `langinfo.h` in this specific case.

#### Language Conformance

| Package | Release | C Std | C++ Std |
|:--------|:--------|:------|:--------|
| OTP | \< 21 | c99 | c++03 |
| OTP | 21+ | c11 | c++11 |
| OpenSSL | 1.0 | c90? | n/a |
| OpenSSL | 1.1 | c99? | n/a |
| OpenSSL | 3.0 | c11? | n/a |
| wxWidgets | 3.0 | gnu99 | gnu++11 |
| wxWidgets | 3.1 | gnu11 | gnu++11 |


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
