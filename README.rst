doh-intel
==========
files formatted for the `Zeek Intelligence Framework <https://docs.zeek.org/en/current/frameworks/intel.html>`_
providing indicators for servers known to offer DNS over HTTPS. Notices will be raised on connection. To receive notices when the DoH server name is looked up in regular DNS, see: 
`extend-if-in <https://github.com/jbaggs/extend-if-in>`_.

doh.intel works with `Zeek Intelligence Framework <https://docs.zeek.org/en/current/frameworks/intel.html>`_ in its standard configuration.
doh-wildcard.intel has been added to allow detection of servers that answer to any sub-domain of the parent domain. (e.g.: "doh.example.com", "foo.doh.example.com", "foo.bar.doh.example.com", etc.)
Use of ``doh-wildcard.intel`` requires the installation of the `wildcard-info <https://github.com/jbaggs/wildcard-info>`_ script. 
If you are using `extend-if-in <https://github.com/jbaggs/extend-if-in>`_, you may also want to update ``if_in_criteria.zeek`` to receive notices on DNS requests for wildcard domains:::

	##! Extended if_in criteria to generate notices on, beyond the initial if_in restrictions.
	module Intel;

	# Extended if_in criteria organized by meta.source, then indicator_type.
	redef extended_if_in = {
        	["doh.servers"] = table([Intel::DOMAIN]=set(DNS::IN_REQUEST),
					[Intel::WILDCARD_DOMAIN]=set(DNS::IN_REQUEST)),
	};


Downloading
-----------
Download directly with the applicable command for your OS.

``wget https://raw.githubusercontent.com/jbaggs/doh-intel/master/doh.intel``

``curl https://raw.githubusercontent.com/jbaggs/doh-intel/master/doh.intel -o doh.intel``

``fetch https://raw.githubusercontent.com/jbaggs/doh-intel/master/doh.intel``
