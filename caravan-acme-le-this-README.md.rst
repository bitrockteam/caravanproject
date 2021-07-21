Caravan ACME LE
===============

TEST!!!! ## Requirements

============================ =======
Name                         Version
============================ =======
                             2.1.2
`acme <#requirement_acme>`__ 
============================ =======

Providers
---------

========================= =======
Name                      Version
========================= =======
                          2.1.2
`acme <#provider_acme>`__ 
                          n/a
`null <#provider_null>`__ 
`tls <#provider_tls>`__   n/a
========================= =======

Modules
-------

No modules.

Resources
---------

+----------------------------------------------------------+----------+
| Name                                                     | Type     |
+==========================================================+==========+
| `acme_certificat                                         | resource |
| e.certificate_auto <https://registry.terraform.io/provid |          |
| ers/vancluever/acme/2.1.2/docs/resources/certificate>`__ |          |
+----------------------------------------------------------+----------+
| `acme_certificate.ce                                     | resource |
| rtificate_from_csr <https://registry.terraform.io/provid |          |
| ers/vancluever/acme/2.1.2/docs/resources/certificate>`__ |          |
+----------------------------------------------------------+----------+
| `acme                                                    | resource |
| _registration.reg <https://registry.terraform.io/provide |          |
| rs/vancluever/acme/2.1.2/docs/resources/registration>`__ |          |
+----------------------------------------------------------+----------+
| `nu                                                      | resource |
| ll_resource.dns_check <https://registry.terraform.io/pro |          |
| viders/hashicorp/null/latest/docs/resources/resource>`__ |          |
+----------------------------------------------------------+----------+
| `tl                                                      | resource |
| s_cert_request.req <https://registry.terraform.io/provid |          |
| ers/hashicorp/tls/latest/docs/resources/cert_request>`__ |          |
+----------------------------------------------------------+----------+
| `tls_priv                                                | resource |
| ate_key.private_key <https://registry.terraform.io/provi |          |
| ders/hashicorp/tls/latest/docs/resources/private_key>`__ |          |
+----------------------------------------------------------+----------+

Inputs
------

+--------+--------------------+--------+-------------+---------------+
| Name   | Description        | Type   | Default     | Required      |
+========+====================+========+=============+===============+
|        | Common             | ``st   | n/a         | yes           |
| `commo |                    | ring`` |             |               |
| n_name |                    |        |             |               |
|  <#inp |                    |        |             |               |
| ut_com |                    |        |             |               |
| mon_na |                    |        |             |               |
| me>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | n/a         | yes           |
| `d     |                    | ring`` |             |               |
| ns_pro |                    |        |             |               |
| vider  |                    |        |             |               |
| <#inpu |                    |        |             |               |
| t_dns_ |                    |        |             |               |
| provid |                    |        |             |               |
| er>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | When using         | ``st   | ``          | no            |
| `aws_p | dns_provider==aws, | ring`` | "default"`` |               |
| rofile | the AWS profile    |        |             |               |
|  <#inp | name               |        |             |               |
| ut_aws |                    |        |             |               |
| _profi |                    |        |             |               |
| le>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | When using         | ``st   | ``""``      | no            |
| `aws   | dns_provider==aws, | ring`` |             |               |
| _regio | the AWS region     |        |             |               |
| n <#in |                    |        |             |               |
| put_aw |                    |        |             |               |
| s_regi |                    |        |             |               |
| on>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | When using         | ``st   | ``""``      | no            |
| `aws_z | dns_provider==aws, | ring`` |             |               |
| one_id | the AWS zone id    |        |             |               |
|  <#inp |                    |        |             |               |
| ut_aws |                    |        |             |               |
| _zone_ |                    |        |             |               |
| id>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | ``""``      | no            |
| `a     |                    | ring`` |             |               |
| zure_c |                    |        |             |               |
| lient_ |                    |        |             |               |
| id <#i |                    |        |             |               |
| nput_a |                    |        |             |               |
| zure_c |                    |        |             |               |
| lient_ |                    |        |             |               |
| id>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | ``""``      | no            |
| `azu   |                    | ring`` |             |               |
| re_cli |                    |        |             |               |
| ent_se |                    |        |             |               |
| cret < |                    |        |             |               |
| #input |                    |        |             |               |
| _azure |                    |        |             |               |
| _clien |                    |        |             |               |
| t_secr |                    |        |             |               |
| et>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | `           | no            |
| `azure |                    | ring`` | `"public"`` |               |
| _envir |                    |        |             |               |
| onment |                    |        |             |               |
|  <#inp |                    |        |             |               |
| ut_azu |                    |        |             |               |
| re_env |                    |        |             |               |
| ironme |                    |        |             |               |
| nt>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | ``""``      | no            |
| `azure |                    | ring`` |             |               |
| _resou |                    |        |             |               |
| rce_gr |                    |        |             |               |
| oup <# |                    |        |             |               |
| input_ |                    |        |             |               |
| azure_ |                    |        |             |               |
| resour |                    |        |             |               |
| ce_gro |                    |        |             |               |
| up>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | Azure              | ``st   | ``""``      | no            |
| `a     |                    | ring`` |             |               |
| zure_s |                    |        |             |               |
| ubscri |                    |        |             |               |
| ption_ |                    |        |             |               |
| id <#i |                    |        |             |               |
| nput_a |                    |        |             |               |
| zure_s |                    |        |             |               |
| ubscri |                    |        |             |               |
| ption_ |                    |        |             |               |
| id>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | ``""``      | no            |
| `a     |                    | ring`` |             |               |
| zure_t |                    |        |             |               |
| enant_ |                    |        |             |               |
| id <#i |                    |        |             |               |
| nput_a |                    |        |             |               |
| zure_t |                    |        |             |               |
| enant_ |                    |        |             |               |
| id>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | The DNS polling    | ``st   | ``""``      | no            |
| `dns_p | interval           | ring`` |             |               |
| olling |                    |        |             |               |
| _inter |                    |        |             |               |
| val <# |                    |        |             |               |
| input_ |                    |        |             |               |
| dns_po |                    |        |             |               |
| lling_ |                    |        |             |               |
| interv |                    |        |             |               |
| al>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | The DNS            | ``st   | ``""``      | no            |
| `dns_p | propagation        | ring`` |             |               |
| ropaga | timeout            |        |             |               |
| tion_t |                    |        |             |               |
| imeout |                    |        |             |               |
|  <#inp |                    |        |             |               |
| ut_dns |                    |        |             |               |
| _propa |                    |        |             |               |
| gation |                    |        |             |               |
| _timeo |                    |        |             |               |
| ut>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``st   | ``"let      | no            |
| `ema   |                    | ring`` | sencrypt@ex |               |
| il_add |                    |        | ample.it"`` |               |
| ress < |                    |        |             |               |
| #input |                    |        |             |               |
| _email |                    |        |             |               |
| _addre |                    |        |             |               |
| ss>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | n/a                | ``     | ``true``    | no            |
| `from_ |                    | bool`` |             |               |
| csr <# |                    |        |             |               |
| input_ |                    |        |             |               |
| from_c |                    |        |             |               |
| sr>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | When using         | ``st   | ``""``      | no            |
| `gcp_p | dns_provider==gcp, | ring`` |             |               |
| roject | the GCP projec ID  |        |             |               |
| _id <# |                    |        |             |               |
| input_ |                    |        |             |               |
| gcp_pr |                    |        |             |               |
| oject_ |                    |        |             |               |
| id>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | When using         | ``st   | ``""``      | no            |
| `g     | dns_provider==gcp, | ring`` |             |               |
| cp_ser | the GCP service    |        |             |               |
| vice_a | account file       |        |             |               |
| ccount |                    |        |             |               |
| _file  |                    |        |             |               |
| <#inpu |                    |        |             |               |
| t_gcp_ |                    |        |             |               |
| servic |                    |        |             |               |
| e_acco |                    |        |             |               |
| unt_fi |                    |        |             |               |
| le>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+
|        | Private key pem    | ``st   | ``null``    | no            |
| `priva |                    | ring`` |             |               |
| te_key |                    |        |             |               |
|  <#inp |                    |        |             |               |
| ut_pri |                    |        |             |               |
| vate_k |                    |        |             |               |
| ey>`__ |                    |        |             |               |
+--------+--------------------+--------+-------------+---------------+

Outputs
-------

+-------------------------------------------------------+-------------+
| Name                                                  | Description |
+=======================================================+=============+
| `certificate_p12 <#output_certificate_p12>`__         | n/a         |
+-------------------------------------------------------+-------------+
|                                                       | n/a         |
| `certifica                                            |             |
| te_p12_password <#output_certificate_p12_password>`__ |             |
+-------------------------------------------------------+-------------+
| `certificate_pem <#output_certificate_pem>`__         | n/a         |
+-------------------------------------------------------+-------------+
| `issuer_pem <#output_issuer_pem>`__                   | n/a         |
+-------------------------------------------------------+-------------+
| `private_key_pem <#output_private_key_pem>`__         | n/a         |
+-------------------------------------------------------+-------------+

.. raw:: html

   <!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
