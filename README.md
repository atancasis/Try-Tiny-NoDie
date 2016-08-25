# NAME

Try::Tiny::NoDie - minimal try/catch with local-disabling of SIGDIE

# SYNOPSIS

Preserves all of [Try::Tiny](https://metacpan.org/pod/Try::Tiny)'s semantics to expect and handle exceptions but
adds a `try_no_die` keyword which behaves exactly just like `try` but with
a locally-disabled `__DIE__` hook.

As such:

    try_no_die {
      die "foo";
    };

is exactly equivalent to:

    try {
      local $SIG{__DIE__} = "IGNORE";
      die "foo";
    };

# DESCRIPTION

This module is primarily designed for developer convenience, for cases
wherein the desired behavior within the scope of the error throwing code
is a nullified `__DIE__` handler.

# FAQ

### Why not add an option to disable `__DIE__` on [Try::Tiny](https://metacpan.org/pod/Try::Tiny)?

Yes, that's possible.

However, as [Try::Tiny](https://metacpan.org/pod/Try::Tiny) aims to preserve compatibility as one of its design
objective, **Try::Tiny::NoDie** holds a different opinion and offers this
option to the developer.

### Why not override the default behavior of `try` instead?

As disabling `__DIE__` within the scope of the error throwing code is a
rather specific corner case, this poses a potential risk when the
developer expects otherwise if the same keyword was to be overriden.

Due to this, a separate `try_no_die` keyword has been added instead.

# AUTHOR

Arnold Tan Casis <atancasis@cpan.org>

# COPYRIGHT

Copyright 2016- Arnold Tan Casis

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

[Try::Tiny](https://metacpan.org/pod/Try::Tiny)
