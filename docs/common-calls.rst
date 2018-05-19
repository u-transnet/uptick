**********************
Commonly Used Commands
**********************

Adding keys
~~~~~~~~~~~

uptick comes with its own encrypted wallet to which keys need to be
added:::

    uptick addkey

On first run, you will be asked to provide a new passphrase that you
will need to provide every time you want to post on the BitShares network.
Using an empty password is not allowed, however, you can used the
`UNLOCK` environmental variable if you need to automatically unlock the
wallet with uptick:::

    UNLOCK="password" uptick transfer ....

List available Keys and accounts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can list the installed keys using:::

    uptick listkeys

This command will give the list of public keys to which the private keys
are available.::

    uptick listaccounts

This command tries to resolve the public keys into account names
registered on the network (experimental).

Configuration
~~~~~~~~~~~~~

``uptick`` comes with its owne configuration:::

    uptick set default_account <account-name>

All configuration variables are provided with ``uptick set --help``
You can see your local configuration by calling::

    uptick configuration

Transfer Assets
~~~~~~~~~~~~~~~

BitShares can be transfered via::

    uptick transfer receipient 100.000 BTS

If ``--author`` is not provided, the *default* account as defined with
``uptick set author`` will be taken.

Buy/Sell Assets
~~~~~~~~~~~~~~~

You can of course sell your assets in the internal decentralized exchange that
is integrated into the BitShares blockchain by using:::

    uptick buy <amount> <asset-to-buy> <price> <asset-to-sell> 
    uptick sell <amount> <asset-to-sell> <price> <asset-to-buy>

Balances
~~~~~~~~

Get an account's balance with::

    uptick balance <account>

If ``<account>`` is not provided, the *default* account will be taken.

History
~~~~~~~

You can get an accounts history by using::

    uptick history <account>

Furthermore you can filter by ``types`` and limit the result by
transaction numer. More information can be found by calling ``uptick
history -h``.


Permissions
~~~~~~~~~~~

Any account permission can be inspected using::

    uptick permissions [<account>]

The take the following form::

    +------------+-----------+-----------------------------------------------------------+
    | Permission | Threshold |                                               Key/Account |
    +------------+-----------+-----------------------------------------------------------+
    |      owner |         2 |                                                fabian (1) |
    |            |           | BTS7mgtsF5XPU9tokFpEz2zN9sQ89oAcRfcaSkZLsiqfWMtRDNKkc (1) |
    +------------+-----------+-----------------------------------------------------------+
    |     active |         1 | BTS6quoHiVnmiDEXyz4fAsrNd28G6q7qBCitWbZGo4pTfQn8SwkzD (1) |
    +------------+-----------+-----------------------------------------------------------+
    |    posting |         1 |                                             streemian (1) |
    |            |           | BTS6xpuUdyoRkRJ1GQmrHeNiVC3KGadjrBayo25HaTyBxBCQNwG3j (1) |
    |            |           | BTS8aJtoKdTsrRrWg3PB9XsbsCgZbVeDhQS3VUM1jkcXfVSjbv4T8 (1) |
    +------------+-----------+-----------------------------------------------------------+

The permissions are either **owner** (full control over the account),
**active** (full control, except for changing the owner), and
**posting** (for posting and voting). The keys can either be a public
key or another account name while the number behind shows the weight of
the entry. If the weight is smaller than the threshold, a single
signature will not suffice to validate a transaction

Allow/Disallow
~~~~~~~~~~~~~~

Permissions can be changed using:::

    uptick allow --account <account> --weight 1 --permission posting --threshold 1 <foreign_account>
    uptick disallow --permission <permissions> <foreign_account>

More details and the default parameters can be found via:::

    uptick allow --help
    uptick disallow --help

Info
~~~~
uptick can read data from the blockchain and present it to the user in
tabular form. It can automatically identify:

* block numbers (``1000021``)
* account names (``uptick``)
* assets (``BTS``)
* public keys (``BTSxxxxxxxxxx``)
* general blockchain parameters

The corresponding data can be presented using:::

    uptick info [block_num [account name [pubkey [identifier [asset]]]]]

