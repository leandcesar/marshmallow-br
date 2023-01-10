==============
Marshmallow-BR
==============

.. raw:: html

   <h1 align="center">
    <img src="https://github.com/leandcesar/marshmallow_br/blob/main/docs/static/logo.png?raw=true"  width="300px" alt="Marshmallow BR"/>
   </h1>

This library provides `Marshmallow`_ fields and validators for Brazilian documents:

* CNH
* CNPJ
* CPF
* Brazilian birth, marriage and death certificates
* Brazilian phone number

Installing
----------

.. code-block:: console

    $ pip install marshmallow-br

Usage
-----

.. code:: py

    from pprint import pprint
    from marshmallow import Schema

    from marshmallow_br import fields


    class Documents(Schema):
        certificate = fields.Certificate(mask=True)
        cnh = fields.CNH(mask=True)
        cnpj = fields.CNPJ(mask=True)
        cpf = fields.CPF(mask=True)
        phones = fields.List(fields.Phone(mask=True, require_ddi=False, require_ddd=True))

    raw_data = {
        "certificate": "12173901552014167634174940702955",
        "cnh": "64076917022",
        "cnpj": "52203670000109",
        "cpf": "98008862068",
        "phones": ["5511999999999", "11999999999", "+55 (11) 99999-9999", "55 11 99999999"],
    }

    data = Documents().load(raw_data)
    pprint(data)

    # {'certificate': '121739.01.55.2014.1.67634.174.9407029-55',
    # 'cnh': '64076917022',
    # 'cnpj': '52.203.670/0001-09',
    # 'cpf': '980.088.620-68',
    # 'phones': ['+55 (11) 99999-9999',
    #             '(11) 99999-9999',
    #             '+55 (11) 99999-9999',
    #             '+55 (11) 9999-9999']}


.. _`Marshmallow`: https://github.com/marshmallow-code/marshmallow