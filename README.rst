doh-intel
==========
files formatted for the `Zeek Intelligence Framework <https://docs.zeek.org/en/current/frameworks/intel.html>`_
providing indicators for servers known to offer DNS over HTTPS. Notices will be raised on connection. To receive notices when the DoH server name is looked up in regular DNS, see: 
`extend-if-in <https://github.com/jbaggs/extend-if-in>`_.

doh.intel works with the `Zeek Intelligence Framework <https://docs.zeek.org/en/current/frameworks/intel.html>`_ in its standard configuration.

doh-wildcard.intel has been added to allow detection of servers that answer to any sub-domain of the parent domain. (e.g.: "doh.example.com", "foo.doh.example.com", "foo.bar.doh.example.com", etc.)
Use of ``doh-wildcard.intel`` requires the installation of the `wildcard-domain <https://github.com/jbaggs/wildcard-domain>`_ script. 
If you are using `extend-if-in <https://github.com/jbaggs/extend-if-in>`_, you may also want to update ``if_in_criteria.zeek`` to receive notices on DNS requests for wildcard domains::

	##! Extended if_in criteria to generate notices on, beyond the initial if_in restrictions.
	module Intel;

	# Extended if_in criteria organized by meta.source, then indicator_type.
	redef extended_if_in = {
        	["doh.servers"] = table([Intel::DOMAIN]=set(DNS::IN_REQUEST),
					[Intel::WILDCARD_DOMAIN]=set(DNS::IN_REQUEST)),
	};

**NOTE: Entries have been removed from doh.intel that partially duplicated coverage of doh-wildcard.intel.**

Downloading
-----------
Intel files may be downloaded directly from the URLs:

``https://raw.githubusercontent.com/jbaggs/doh-intel/master/doh.intel``

``https://raw.githubusercontent.com/jbaggs/doh-intel/master/doh-wildcard.intel``
