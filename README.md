# CS360MobileArchitech-Programming
Andriod warehouse inventory app (java + SQLite) with a dynamic database inventory grid, full CRUD, and SMS restock alerts gated by Android's runtime permission system. Built for SNHU CS-360

The inventory tracker app is an Android app for small warehouse and stickroom staff to manage inventory without a full ERP system. It addresses three core user needs. Secure login so only staff can make changes, a live view of the current stock that ipdates the moment someone changes it, and a way to know immediately when an item runs out.

The app needed four screens to support those needs. A login screen, an account creation screen, the inventory grid itself, and an sms alert settings screen. Rather than a satic list, it is built to chnage dynamically from whatever the database contains with the + and - remove controls on each row without having to chnage screens. The sms screen was separated from the main inventory screen so permission related decisions are not buried  as a side effect of some other options.

I built the data layer first, a single databasehelper class handling read/write before putting it on the screen. Login, account creation and inventory management were each just calling into somehting already tested rather than three separate sources of bugs. I worked one method and one behavior at a time, write, run, comfirm it behaved right, then moved on to the next piece. I will apply this to future projects rather than all at once.

I tested a lot int he android emulator rather then relying on thinking the code was correct. I had several bugs that only became visible by actuallu runnning the app and noticing the behavior was wrong. One example, the inventory items quantity stopped updaing after the first button tap because the database and the screen were both being updated but in the memory object holding the value never was. That bug was invisible when writing the code but later showed up when testing the app. 

I had to problem solve when making the inventory grid dynamic. The starting layout had three rows hard coded into the xml which meant items could never actuallu be added or removed. I had to query the database for the current item list, then build each rows text, buttons, click listeners at runtime instead of writing them in the xml. That also had a problem show up, if the screen would rebuild itself, items would duplicate instead of refreshing.

