# SFDX  App

This repo demonstrates a bug with Salesforce DX observed in Winter '19
and API 44.0, regarding the ability to push source to new scratch orgs
with field history tracking enabled

## Dev, Build and Test

1. Clone this repo
2. Create a new scratch org using **config/project-scratch-def.json**
3. Push source to the new scratch org using `sfdx force:source:push`

```txt
=== Push Errors
PROJECT PATH                                                                 ERROR
───────────────────────────────────────────────────────────────────────────  ───────────────────────────────────────────────────────────────────
force-app/main/default/objects/Account/fields/BillingAddress.field-meta.xml  The entity: Account does not have history tracking enabled (105:13)
force-app/main/default/objects/Account/fields/Name.field-meta.xml            The entity: Account does not have history tracking enabled (131:13)
```

The expected outcomes are as follows.

* No errors are reported
* Field history tracking is enabled for the Account object in the scratch org
* Changes to Billing Address and Account Name are tracked on the Account object
  in the scratch org

Interestingly enough, if the **Contact.object-meta.xml** file is deleted
from the project directory, the errors go away. The errors also disappear
if the `enableHistory` value is changed to "false" in the same file.

## Resources

* "[Push Source to the Scratch Org][1]." _Salesforce DX Developer Guide_.

[1]: https://developer.salesforce.com/docs/atlas.en-us.sfdx_dev.meta/sfdx_dev/sfdx_dev_push_md_to_scratch_org.htm
