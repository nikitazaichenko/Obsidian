On Windows 2019 you can get this error trying to opening some setting.

![](https://www.lavatelli.it/wp-content/uploads/2020/04/ximage.png.pagespeed.ic.JtUBelItAN.webp)

To resolve please run gpedit.msc to open Group Policy Editor, then switch to Computer Configuration—> Windows Settings—> Security Settings —> Local Policies—> Security Options, then enable “User Account Control: Admin Approval Mode for the Built-in Administrator account”.

After all restart Windows to take effect.