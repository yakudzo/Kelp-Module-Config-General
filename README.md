# NAME

Kelp::Module::Config::General - [Config::General](https://metacpan.org/pod/Config::General) as config module for your Kelp applications.

# SYNOPSIS

    # app.psgi
    use MyApp;
    my $app = MyApp->new( config_module => 'Config::General' );
    $app->run;

# DESCRIPTION

This module provides support of [Config::General](https://metacpan.org/pod/Config::General) as your `Kelp::Module::Config` module.

[Config::General](https://metacpan.org/pod/Config::General) module is loaded with following configuration options:

    -ForceArray      => 1,
    -IncludeAgain    => 1,
    -InterPolateVars => 1,

Because [Config::General](https://metacpan.org/pod/Config::General) provides key/value interface you are not able to create array of arrays for your default [Kelp::Module::Logger](https://metacpan.org/pod/Kelp::Module::Logger) configuration. This module does it for you but only in this situation.

Example:

    modules = [ Logger ]
    
    <modules_init Logger>
      <outputs Screen>
         name      debug
         min_level debug
         newline   1
         binmode   :encoding(UTF-8)
      </outputs>
      <outputs Screen>
         name      error
         min_level error
         newline   1
         stderr    1
         binmode   :encoding(UTF-8)
      </outputs>
    </modules_init>

    becomes:

    {
        modules => [ 'Logger' ],
    },
    {
        modules_init => {
            Logger => [
                [
                    'Screen',
                    name      => 'debug',
                    min_level => 'debug',
                    newline   => 1
                    binmode   => ':encoding(UTF-8)'
                ], [
                    'Screen',
                    name      => 'error',
                    min_level => 'error',
                    newline   => 1,
                    stderr    => 1,
                    binmode   => ':encoding(UTF-8)'
                ]
            ],
        }
    }

# AUTHOR

Konstantin Yakunin <twinhooker@gmail.com>

# COPYRIGHT

Copyright 2017- Konstantin Yakunin

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO
