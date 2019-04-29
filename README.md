[![Cpan license](https://img.shields.io/cpan/l/WebService-IPStack.svg)](https://metacpan.org/release/WebService-IPStack)
[![Cpan version](https://img.shields.io/cpan/v/WebService-IPStack.svg)](https://metacpan.org/release/WebService-IPStack)

# NAME

WebService::IPStack - Perl library for IPStack's Geolocation API,
https://ipstack.com.

# SYNOPSIS

    use WebService::IPStack;

    my $ipstack = WebService::IPStack->new(api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxx32');
    $ipstack->lookup('8.8.8.8');

# DESCRIPTION

WebService::IPStack is a Perl library for obtaining Geolocation information on
IPv4 or IPv6 address.

# DEVELOPMENT

Source repo at [https://github.com/kianmeng/webservice-ipstack](https://github.com/kianmeng/webservice-ipstack).

How to contribute? Follow through the [CONTRIBUTING.md](https://github.com/kianmeng/webservice-ipstack/blob/master/CONTRIBUTING.md) document to setup your development environment.

# METHODS

## new($api\_key, \[$api\_plan\])

Construct a new WebService::IPStack instance.

### api\_key

Compulsory. The API access key used to make request through web service.

### api\_plan

Optional. The API subscription plan used when accessing the API. There are four
subscription plans: free, standard, pro, and pro\_plus. The default subscription
plan is 'free'. The main difference between free and non-free subscription
plans are HTTPS encryption protocol support and additional information.

    # The API request URL is http://api.ipstack.com/
    my $ipstack = WebService::IPStack->new(api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxx32');
    print $ipstack->api_url;

    # The API request URL is https://api.ipstack.com/
    my $ipstack = WebService::IPStack->new(
        api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx32',
        api_plan => 'standard'
    );
    print $ipstack->api_url;

### api\_url

The default API hostname and path. The protocol depends on the subscription plan.

## lookup($ip\_address, \[%params\])

Query and get an IP address information. Optionally you can add more settings
to adjust the output.

    my $ipstack = WebService::IPStack->new(api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxx32');
    $ipstack->lookup('8.8.8.8');

    # With optional parameters.
    $ipstack->lookup('8.8.8.8', {hostname => 1, security => 1, output => 'xml'});

## bulk\_lookup($ip\_address, \[%params\])

Only for paid subscription plans (standard, pro, or pro\_plus).  Query and get
multiple IP addresses information. Optionally you can add more settings to
adjust the output.

    my $ipstack = WebService::IPStack->new(
        api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxx32',
        api_plan => 'standard'
    );
    $ipstack->bulk_lookup(['8.8.8.8', '8.8.4.4']);

    # With optional parameters.
    $ipstack->bulk_lookup(['8.8.8.8', '8.8.4.4'], {language => 'zh'});

## check(\[%params\])

Look up the IP address details of the client which made the web service call.
Optionally you can add more settings to adjust the output.

    my $ipstack = WebService::IPStack->new(api_key => '1xxxxxxxxxxxxxxxxxxxxxxxxxxxxx32');
    $ipstack->check();

    # With optional parameters.
    $ipstack->check({hostname => 1, security => 1, output => xml});

# AUTHOR

Kian Meng, Ang <kianmeng@users.noreply.github.com>

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2019 Kian Meng, Ang.

This is free software, licensed under:

    The Artistic License 2.0 (GPL Compatible)
