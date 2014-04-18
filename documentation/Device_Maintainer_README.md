# Device Maintainer Guidelines and Expectations

##### This is not a tutorial to port AOKP to your device, this is a tutorial for the already skilled to become officially supoported!

Getting Your Device Supported
---

There are a few things we expect to see:

##### [vendor_aokp](https://github.com/AOKP/vendor_aokp)
```
Our vendor will need a new .mk file for your device along with the other apprpriate edits to the products folder.
Your device must be added to vendorsetup.sh for nightlies to run for it!
```
[Example](https://github.com/AOKP/vendor_aokp/commit/4e45c7351eb49561283080dd94c311e27f61dd8d)

##### [vendor_(manufacturer)](https://github.com/AOKP?query=vendor_)
``` 
The vendors hold proprietary binaries for each device and when a new device is brought
into AOKP its own proprietary binaries will need to be submitted to its vendor.
As you can see they are named by manufacturer. 
```
[Example](https://github.com/AOKP/vendor_htc/commit/e4009c6c072e237af8fe16e7689087c7b5db7620)

##### [platform_manifest](https://github.com/AOKP/platform_manifest.git)
```
The manifest is where everything comes together:

We want to see all necessary device repos pulled from AOKP, if they are not being maintained by CyanogenMod
or another project, as they will be forked to our Github.
All device repos to be forked to our Github should be linked in the commit message.
All repos added to the manifest must follow our alphabetical and grouping scheme.
Please link all related submissions in this commit as well.
```

##### *We expect to see proper commit authrship and credit*!

##### Note: The extras, such as the related submissions and links to projects to be forked will be editted out just before merging.

***

After the Merge
---

You will most likely be privately contacted by an AOKP member soon after or before
the merge of your device and be brought into communication with the rest of the
team via Google Hangouts or our maling list.

##### Once the device is merged into AOKP our expectations are as follows:

```
Your device must remain buildable with AOKP sources for every nightly.
Your device must remain relatively up to date with CyanogenMod if the repos are originally based off of theirs.
Your device must be updated with the latest version of Android if possible.
Communicate with the team on the status of your devices.
Be willing to collaborate with the team on various matters such as adding features,
fixing bugs, reviewing patches, and helping others.
```
