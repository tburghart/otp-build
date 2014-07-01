# OTP Build Script

A script to build Erlang/OTP.

## Origin

Sometime in the middle of 2014 I started gathering together the assorted scripts and commands I'd
been using to build Erlang/OTP for experimentation into a marginally neater collection.
Some of that eventually went into scripts in the [local_env][LocalEnv] repo, and serves as the
basis of the primary script here.

### Why Not Kerl?

[kerl][Kerl] _was_ around when I started tinkering with the ancestors of this script, and I did use
it enough times to determine I wanted better control over the build process, particularly on Macs
where I was doing my primary building at that time.

## License

To the extent anyone cares, consider it all covered by this highly permisive [license][License].

  [Kerl]:       https://github.com/kerl/kerl
  [LocalEnv]:   https://github.com/tburghat/local_env
  [OTP]:        https://github.com/erlang/otp
  [License]:    LICENSE
