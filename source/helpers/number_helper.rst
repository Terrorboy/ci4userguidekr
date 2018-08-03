#############
Number Helper
#############

The Number Helper file contains functions that help you work with
numeric data in a locale-aware manner.

.. contents::
  :local:

.. raw:: html

  <div class="custom-index container"></div>

Loading this Helper
===================

This helper is loaded using the following code::

	helper('number');

When Things Go Wrong
====================

If PHP's internationalization and localization logic cannot handle
a value provided, for the given locale and options, then a
``BadFunctionCallException()`` will be thrown.

Available Functions
===================

The following functions are available:

.. php:function:: number_to_size($num[, $precision = 1[, $locale = null])

    :param	mixed	$num: Number of bytes
    :param	int	$precision: Floating point precision
    :returns:	Formatted data size string, or false if the provided value is not numeric
    :rtype:	string

    Formats numbers as bytes, based on size, and adds the appropriate
    suffix. Examples::

        echo number_to_size(456); // Returns 456 Bytes
        echo number_to_size(4567); // Returns 4.5 KB
        echo number_to_size(45678); // Returns 44.6 KB
        echo number_to_size(456789); // Returns 447.8 KB
        echo number_to_size(3456789); // Returns 3.3 MB
        echo number_to_size(12345678912345); // Returns 1.8 GB
        echo number_to_size(123456789123456789); // Returns 11,228.3 TB

    An optional second parameter allows you to set the precision of the result::

	    echo number_to_size(45678, 2); // Returns 44.61 KB

    An optional third parameter allows you to specify the locale that should
    be used when generating the number, and can affect the formatting. If no
    locale is specified, the Request will be analyzed and an appropriate
    locale taken from the headers, or the app-default::

        // Generates 11.2 TB
        echo number_to_size(12345678912345, 1, 'en_US');
        // Generates 11,2 TB
        echo number_to_size(12345678912345, 1, 'fr_FR');

    .. note:: The text generated by this function is found in the following
		language file: *language/<your_lang>/Number.php*

.. php:function:: number_to_amount($num[, $precision = 1[, $locale = null])

    :param	mixed	$num: Number to format
    :param	int	$precision: Floating point precision
    :param  string $locale: The locale to use for formatting
    :returns:	A human-readable version of the string, or false if the provided value is not numeric
    :rtype:	string

    Converts a number into a human-readable version, like **123.4 trillion**
    for numbers up to the quadrillions. Examples::

        echo number_to_amount(123456); // Returns 123 thousand
        echo number_to_amount(123456789); // Returns 123 million
        echo number_to_amount(1234567890123, 2); // Returns 1.23 trillion
        echo number_to_amount('123,456,789,012', 2); // Returns 123.46 billion

    An optional second parameter allows you to set the precision of the result::

        echo number_to_amount(45678, 2); // Returns 45.68 thousand

    An optional third parameter allows the locale to be specified::

        echo number_to_amount('123,456,789,012', 2, 'de_DE'); // Returns 123,46 billion

.. php:function:: number_to_currency($num, $currency[, $locale = null])

    :param mixed $num: Number to format
    :param string $currency: The currency type, i.e. USD, EUR, etc
    :param string $locale: The locale to use for formatting
    :returns: The number as the appropriate currency for the locale
    :rtype: string

    Converts a number in common currency formats, like USD, EUR, GBP, etc::

        echo number_to_currency(1234.56, 'USD');  // Returns $1,234.56
        echo number_to_currency(1234.56, 'EUR');  // Returns £1,234.56
        echo number_to_currency(1234.56, 'GBP');  // Returns £1,234.56
        echo number_to_currency(1234.56, 'YEN');  // Returns YEN1,234.56

.. php:function:: number_to_roman($num)

    :param string $num: The number want to convert
    :returns: The roman number converted from given parameter
    :rtype: string

    Converts a number into roman::

        echo number_to_roman(23);  // Returns XXIII
        echo number_to_roman(324);  // Returns CCCXXIV
        echo number_to_roman(2534);  // Returns MMDXXXIV

    This function only handles numbers in the range 1 through 3999.
    It will return null for any value outside that range .