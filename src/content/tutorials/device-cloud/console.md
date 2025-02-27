---
word: Console
title: Console
order: 31
shared: true
columns: two
layout: tutorials.hbs
description: Web-based management for your Particle IoT devices
---


# Console

The [Particle Console](https://console.particle.io) is your
centralized IoT command center. It provides interfaces to make
interacting with and managing Particle devices easy. This guide is
divided into two main sections, [tools for developers](#developer-tools)
and [tools to manage product fleets](#product-tools).

**Note:** The Console does not yet work in Microsoft Internet Explorer including Edge. Please use another browser, such as Chrome or Firefox, to access the Console. If you're experiencing rendering issues, turn off any ad blocking extensions you may be using.

## Developer Tools

While actively developing an IoT project or product, the Console offers
many helpful features to make prototyping a breeze. See the last time a
device connected, debug a firmware issue by observing event logs,
set up a webhook to send data to an external service, and more.

### Devices

The Devices page allows you to see a list of the devices associated with
your account. Here, you can see specific information about each device,
including it's unique Device ID, it's name, the type of device (i.e.
Photon or Electron) the last time it connected
to the Particle cloud, and whether or not the device is currently
online.

<img src="{{assets}}/images/console/devices-view.png"
class="full-width"/>

You can also take certain actions on devices from this view, such as
renaming the device and unclaiming it from your account.

Unclaiming a cellular device removes it from your account, but does not stop billing. As the claiming status and SIM are separate, you must also pause or release ownership of your SIM to stop billing.

### Event Logs

The Logs feature provides a clean interface to view event information in real-time, just from your devices. We're hoping that this is handy both while debugging code during development, and checking out recent activity on your device once you power-on your finished project. Tailored around improving the experience of browsing logs, the page provides a handful of tools, like filtering, modifiers which enable you to narrow down your search for events, making it easier to view only the data that is relevant to you. In this view, you'll only see events that come in while the browser window is open.

To visit the page go to [https://console.particle.io/events](https://console.particle.io/events)

<img src="/assets/images/eventlogs/full.png" class="full-width" />

#### Logs

The left side of the page contains a real-time log of events passing through the cloud. You'll get the name, data, timestamp and the device name associated with each event as it comes in. Oh Yeah! And, if you click on the event, you can see the event data.

#### How to publish events

Publishing events can be achieved in multiple ways:
- Using `particle.publish` in firmware ([docs](/cards/firmware/cloud-functions/particle-publish/))
- Using Particle API JS's `publishEvent` ([docs](/reference/SDKs/javascript/#publishevent))
- Using the Publish event button in the Event Logs page:

<img src="/assets/images/eventlogs/publish.png" class="full-width" />

#### Filtering the events

Filters let you narrow down your search and only see events that are relevant.

You can filter the events by writing anything in the input. Your query will be compared with the event name, data, publisher, and date.
<img src="/assets/images/eventlogs/filter_word.gif" class="full-width" />

#### Modifiers

Besides writing in the input, you can use modifiers to narrow down your search even further. You can see the list of modifiers by pressing the Advanced button.

<img src="/assets/images/eventlogs/filters.png" class="full-width" />

- `device` Filter by device ID (example: `device:34003d001647353236343012`). The `device` modifier is not usable when viewing a device's individual page, as the stream is already listening only for events coming from that device.
- `event` Filter by event name (example: `event:status`)
- `range` Only show events that have a number value between min and max (`range:min-max`, example: `range:20-100`)
- `data` Filter by data (example: `data:device-is-ok`)

Modifiers can be grouped: `device:34003d001647353236343012 event:temperature range:30-50`

** Note: Having multiple modifiers of the same type is not yet supported (you can not filter by 2 device IDs) **

You can combine modifiers with a query. In this example, we combine the query '35' with the modifier 'event:temperature'. The page will only show events named `temperature` that have `35` as their data.
<img src="/assets/images/eventlogs/filter_multiple.png" class="full-width" />

#### Viewing event data

To view more details about an event, click on it. If the event data is a valid JSON string, it will be displayed in a way that makes it easier to read and understand.

<img src="/assets/images/eventlogs/eventdata_pretty.png" />

To view the raw version of the JSON, click on the `RAW` button.

<img src="/assets/images/eventlogs/eventdata_raw.png" class="full-width" />

You can copy the data to the clipboard if you click on the copy button.

** Note: You can also navigate through the event list by using the up and down arrow keys **

#### Clearing the event logs

You can empty the list of received events by pressing on the Clear button.

#### Pausing the event stream

If lots of events are coming through, you can put events in a queue by clicking on the Pause button. This should help you navigate through the list of events that you have already received.

To make the events from the queue visible click on the Play button.

<img src="/assets/images/eventlogs/queue.png" class="full-width" />

### Integrations

Integrations allow you to send data from your Particle devices to
external tools and services. The Console provides an interface to
create, view, edit, and delete Particle integrations.

<img src="{{assets}}/images/console/integrations-view.png"
class="full-width"/>

For more information on how to start using integrations, you should
check out:

- [Webhooks
guide](/tutorials/device-cloud/webhooks/)
- [Webhooks
tutorial](/tutorials/device-cloud/webhooks/)
- [Azure IoT Hub
tutorial](/tutorials/integrations/azure-iot-hub/)
- [Google Cloud Platform
tutorial](/tutorials/integrations/google-cloud-platform/)

### Billing

The **Billing** page in the console now includes your personal sandbox. The sandbox can include up to 100 cellular and Wi-Fi devices (in any combination, not to exceed 100 total), free of charge. For the Growth Tier, this is in addition to devices included in your Growth Tier blocks.

From this page you can view the total number of devices and data operations consumed by your free sandbox devices.

<img src="{{assets}}/images/console/sandbox.png" class="full-width"/>


## Product Tools

For many using Particle, the end-goal is to move from a single prototype
to a professional deployment of thousands or millions of units in the
field. When you begin making this transition to managing a larger fleet
of devices, you'll find yourself asking questions like:

- _How many_ of my devices are online right now?
- _Which_ firmware version is running on each device?
- _Who_ of my customers are using their devices, and who isn't?
- _Who_ in my company has access to this fleet, and what information can they
access?

This is where creating a Particle product is vital to ensure scaling can
happen seamlessly and successfully.

Luckily, the Particle Console is designed to give you full visibility into the
state of your product fleet, and provide a centralized control panel to change how
devices are functioning. It allows you and a team to manage firmware running on your devices, collect and analyze product data, and manage team permissions from a single administrative interface.

The first step to get started is understanding the differences between your
personal devices and those added to a Product.

### Devices vs Product Devices

Up until now, you've been an individual user of Particle. Your devices belong to
you, and you can only act upon one device at a time.

When you create a **Product**, you'll have a few additional important concepts available to you: **devices**, **team members** and **customers**.

First, you'll set up a **Product**, the overarching group responsible for the
development of your Internet of Things products.

Defining a Product is what unifies a group of homogeneous devices together, and your Product can be configured to function exactly how you
envision.

Each Product has its own fleet of associated **devices**. Any hardware
on the Particle Device Cloud including the PØ, P1,
Photon, and Electron, could be used inside a Product, but it's important to note that only one type of device will be in each Product

**Customers** own a device, and have permissions to control
their device. You will define the extent of their access to the device when you
configure your Product. 

For cellular devices, it is also common to have all devices claimed to a single account, rather than using individual customer accounts. It is also possible to use unclaimed product devices.

Your Product also has **team members** with access to the Console.

It is important to note that *team members* and *customers* have different levels of access. For instance, only *team members* will typically be able to send an over-the-air firmware update, while *customers* may have the ability to control their own product. These access levels will be controlled through the Console.

### Defining a product

Our cloud platform thinks that all devices are *Photons*, *Electrons*, or *Cores* — unless it's told otherwise. Now's the time to define your own product within the platform and tell us a bit about how that product should behave.

*Photons* are development kits. They're designed to be easy to reprogram and run a variety of software applications that you, our users, develop.

*Your product* is (probably) not a development kit. While some of the characteristics of the development kits will carry over, you're going to want to make a bunch of changes to how your product works. These include:

- Limiting access (e.g. only certain people can reprogram them)
- Collecting bulk data, events, errors, and logs from all of your devices
- Distributing firmware updates in a controlled fashion

To create a product, return to your personal console page and click on the **New Product** button.

![Your product page](/assets/images/products-page.png)

This will open up a modal where you can add basic details about your product:

![A new product](/assets/images/new-product-modal.png)

You now have your very first Particle product! Woot!

### Adding team members

Now that you have created a Product successfully, it's time to add your coworkers and friends that are collaborating with you on your IoT product. Adding a team member will give them full access to your Product's Console.

To do this, click on the *team icon* (<i class="ion-person-stalker"></i>) on the sidebar of your Product Console. This will direct you to the team page, where you can view and manage team members. Right now, your username should be the only one listed as a member of the Product. To add a new team member, just click the *Invite team member* button pictured below:

![Team page](/assets/images/team-page.png)

Clicking this button will open up a modal where you can invite a team member by email address. Before inviting a new team member, **make sure that they already have a Particle account with the email address you will be using to invite them to the Product**. 

![Invite team member](/assets/images/invite-team-member.png)
<p class="caption">The invite team member modal</p>

Once your team member is successfully invited, they will receive an email notifying them of their invitation. The next time they log into their Console, they will have the option of accepting or declining the invitation. Remember that you can have up to 5 team members in the free Prototype tier, so go send some invites!

Nice! Now you have a Product with a team.

### Your Product ID

When you created your product, a unique numeric ID was assigned to it. This small piece of information is *very, very important* to you as a product creator, and it will be used countless times during the development and manufacturing process for your product. You will be able to find your product's ID at any time in the navigation bar when viewing information about your product:

![A new product](/assets/images/product-id.png)
<p class="caption">Your product ID is marked with a key icon</p>

This ID will be used by the Particle Device Cloud to identify which devices belong to your Product, and subsequently it is part of what empowers you to manage firmware running on those devices *en masse*.

When working with devices that belong to your Product, it is important to note that this product ID must be compiled into the firmware that is running on each device. The product ID that the device reports to the cloud from its firmware will determine which Product it requests to become a part of. This will be covered more in-depth in the [rollout firmware](#rollout-firmware) section below.

### Adding Devices

Now that you have your Product, it's time to import devices. Importing devices will assign them to your Product and allow you to start viewing and managing these devices within your Product Console.

For any product you may be developing, you likely have one or more Particle development kits (i.e. a Photon) that you have been using internally for prototyping purposes. We strongly recommend importing these devices into your Product, and using them as your *development group*.

In addition, you'll want to have a *test group* of devices to serve as the guinea pigs for new versions of product firmware. You should get into the habit of uploading a new version of firmware to your product, and flashing it to your test group to ensure your code is working as expected. This too will be covered more in-depth in the [rollout firmware](#rollout-firmware) section below.

To import devices, click on the Devices icon in your product sidebar, then click on the "Import" button.

![Your product's devices](/assets/images/devices-page.png)

To allow you to import devices in bulk, we allow you to upload a file containing multiple device IDs. Create a `.txt` file that contains all of the IDs of devices that you would like to import into your product, one on each line. [Not sure what your device ID is?](/tutorials/developer-tools/cli/#running-from-source-advanced-particle-identify) *You cannot register devices that have already been 'claimed' by someone outside of your team; all of these devices must either belong to a team member or belong to no one*. The file should look something like this:

```
55ff6d04498b49XXXXXXXXXX
45f96d06492949XXXXXXXXXX
35ee6d064989a9XXXXXXXXXX
```

Where each line is one Device ID. Once you have your file ready, drop it onto the file selector in the import devices dialog box.

![Import devices modal](/assets/images/import-devices.png)

As noted at the bottom of the dialog box, if you previously rolled out
firmware, those newly imported devices will be updated over the air to
that firmware next time they connect to the Particle Device Cloud.

### Rollout Firmware

One of the most valuable features of a Particle product is being able
to seamlessly manage firmware on a fleet of IoT devices. You now have
the ability to continuously improve how a device functions after
deployment. In addition, product firmware management allows you to
quickly and remotely fix bugs identified in the field, fleet-wide.

This happens through **firmware releases**, which targets some or all of
a device fleet to automatically download and run a firmware binary.

#### Recommended development flow

When releasing firmware your fleet, it's helpful to first understand
Particle's recommended release flow. This flow has been designed to minimize
risk when deploying new firmware to devices:

<img src="/assets/images/release-firmware-flow.png" class="full-width" />
<p class="caption">The recommended flow for releasing firmware</p>

1. The first step of the release flow is using [**development
devices**](/tutorials/product-tools/development-devices/) to rapidly develop and iterate on product firmware. These are special
product devices marked specifically for internal testing.
This gives you the flexibility to experiment with
new firmwares while still simulating behaviors of deployed devices in
the production fleet. For information on marking a device as a
development devices, check out [the
guide](/tutorials/product-tools/development-devices/#marking-a-development-device).

2. When you have finalized a firmware that you feel confident in releasing
to your fleet, [**prepare the binary and upload it to your
product**](#preparing-a-binary).

3. Before releasing, you will need to ensure that the uploaded product
firmware is running on at least one device in your product fleet.
Your development device(s) may already be running the firmware,
but we also recommend [**locking one or more devices**](#locking-firmware)
to the newly updated firmware and ensure that it re-connects
successfully to the cloud. This is because locking more closely
represents a release action, with the specific firmware being delivered
to a product device.

4. [**Mark the firmware as released**](#releasing-firmware). This will
target product devices to automatically download and run the firmware.
The Particle Device Cloud will respect the [precedence
rules](#firmware-precedence-rules) to determine which firmware is
delivered to a given device. If you are on the Enterprise plan with
access to [device groups](/tutorials/product-tools/device-groups/),
you can more safely roll out the firmware by targeting a subset of the
fleet for release.

The rest of this section contains details around how to go through this
process.

#### Development devices

Please visit the [guide on development
devices](/tutorials/product-tools/development-devices/) for
information on this feature.

#### Preparing a binary

Click the Firmware icon in the left sidebar to get started. This will direct you to your product's firmware page, your centralized hub for viewing and managing firmware for your product's devices. If you haven't yet uploaded any firmware for this Product, your page will look like this:

<img src="/assets/images/firmware-page.png" class="full-width"
alt="Firmware page"/>

If you have been using the [Web IDE](/tutorials/developer-tools/build/) to
develop firmware, you are used to the process of writing, compiling, and
then flashing firmware. You will follow the same high-level process
here, but altered slightly to work with a fleet of devices. The first thing you'll need to do is compile a *firmware binary* that you will upload to your Console.

Unlike compiling a binary for a single device, it is critical that the **product ID** and a **firmware version** are included in the compiled binary. Specifically, you must add `PRODUCT_ID([your product ID])` and `PRODUCT_VERSION([version])` into the application code of your firmware. This is documented fully [here](https://github.com/particle-iot/device-os/blob/develop/docs/build.md#product-id).

Add these two "macros" near the top of your main application `.ino`
file, below `#include "Particle.h"` if it includes that line. Remember
that your [product ID](#your-product-id) can be found in the navigation
of your Console. The firmware version must be an integer that increments
each time a new binary is uploaded to the Console. This allows the
Particle Device Cloud to determine which devices should be running which firmwares.

Here is an example of Blinky with the correct product and version details:

```
PRODUCT_ID(94);
PRODUCT_VERSION(1);

int led = D0;  // You'll need to wire an LED to this one to see it blink.

void setup() {
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH);   // Turn ON the LED pins
  delay(300);               // Wait for 1000mS = 1 second
  digitalWrite(led, LOW);    // Turn OFF the LED pins
  delay(300);               // Wait for 1 second in off mode
}
```

#### Compiling Binaries

If you are using Particle Workbench, follow the instructions to use the [**Particle: Cloud Compile**](/tutorials/developer-tools/workbench/#particle-cloud-compile) or [**Particle: Compile Application (local)**](/tutorials/developer-tools/workbench/#particle-compile-application-local-) to create a firmware binary.


If you are in the Web IDE, you can easily download a compiled binary by
clicking the code icon (<i class="ion-code"></i>) in your sidebar. You
will see the name of your app in the pane, along with a download icon
(shown below). Click the download icon to compile and download your current binary.

![Compile firmware](/assets/images/ide-compile.png)
<p class="caption">Compile and download a product binary from the web IDE</p>

Once you have a binary ready to go, it's time to upload it to the Console!

#### Uploading firmware

Back on the firmware page, click on the **Upload** button in the top-right corner of the page. This will launch the upload firmware modal:

![Upload firmware](/assets/images/upload-firmware.png)

A few things to keep in mind here:

* The firmware version that you enter into this screen **must match** what you just compiled into your binary. Madness will ensue otherwise!
* You should give your firmware a distinct title that concisely describes how it differs from other versions of firmware. This name will be important in how firmware is rolled out to devices
* Attach your newly compiled `.bin` file in the gray box

Click upload. Congrats! You've uploaded your first version of product firmware! You should now see it appear in your list of firmware versions.

![Product firmware version](/assets/images/product-firmware.png)
<p class="caption">Your firmware version now appears in your list of available binaries</p>

You can update the details of your product firmware version by clicking
Edit when hovering over that firmware version.

If you find a problem with your firmware version during testing, you can
delete the firmware version, recompile it and reupload it. It is only
possible to delete a firmware version before marking it as released.

![Product firmware editor](/assets/images/product-firmware-editor.png)
<p class="caption">Edit the details of your firmware version or delete an unreleased version</p>

#### Releasing firmware

Time to flash that shiny new binary to some devices! Notice that when
you hover over a version of firmware, you have the ability to
**release firmware**. Releasing firmware is the mechanism by which any
number of devices can receive a single version of firmware
without being individually targeted.

Imagine identifying a bug in your firmware and pushing out a fix to
thousands of devices that are out in the field. Or, consider the
possibility of continuing to add new capabilities to your fleet connected
devices, even after being deployed. It is all possible via releasing
firmware.

As a product creator, you can choose to release firmware to *some* or *all* of your
product fleet. Releasing a firmware as the **product default** sets the
firmware as the default version available to *all*
devices in the fleet to download and run.

To start the release process, place your cursor over the firmware you
want to release and click **Release firmware**:

<img class="full-width" src="/assets/images/release-firmware-list.png" />

A modal will appear, asking you to confirm the action you are about to
take:

![Release firmware confirmation](/assets/images/release-firmware-confirmation.png)
<p class="caption">Always confirm the version, targeted group(s) and impacted devices
before releasing firmware to your device fleet to ensure you are taking
the desired action.</p>

*Impacted devices* refers specifically to the number of devices
that will receive an OTA firmware update as a direct result of this
action. Keep in mind  that releasing firmware always presents risk. Anytime the code on a
device is changed, there is a chance of introducing bugs or regressions.
As a safeguard, **a firmware version must be successfully running on at
least one device before it can be released**.

When you have confirmed the release is what you have intended, click the
**Release this firmware** button. Note that the devices will not receive the firmware immediately;
instead, they will be targeted for an over-the-air update the next time
they start a new secure session with the cloud (this is called a
*handshake*).

It is also possible to release firmware to a subset of your product
fleet, using [device
groups](/tutorials/product-tools/device-groups/). For more
information on fine-grained firmware management, please check out
[the guide](/tutorials/product-tools/device-groups/) on device
groups.

#### Locking firmware

In many cases, you may want to force a device to download and run a specific
version of product firmware. This is referred to as **locking** the
device. You can lock a device to a new version of product
firmware to test it before releasing the firmware to the fleet.

To lock a device to a firmware, find the device on your product's
devices view <i class="im-devices-icon"></i>. Click on the device, which
will take you to the device details view. Click on the **Edit** button:

<img class="full-width" alt="Edit device" src="/assets/images/edit-device.png" />

This will allow you to edit many aspects of the device's state,
including the firmware it is targeted to run. Find the **Firmware**
section, select a version of firmware you want to lock the device to,
and click the **Lock** button as sown below:

<img class="full-width" alt="Lock device firmware"
src="/assets/images/lock-firmware.png" />

If the device is currently online, you can optionally immediately
trigger an OTA update to the device by checking *Flash now* next to the
lock button. Otherwise, the device will download and run the locked
firmware the next time it handshakes with the cloud (starts a new secure
session, most often on reset).

Once the device downloads and runs the locked firmware, it will no
longer be targeted by the Particle cloud for automatic firmware updates,
until it is unlocked. For more details, please read the [firmware
precedence rules](#firmware-precedence-rules).

#### Unlocking firmware

Unlocking a product device breaks its association with the locked
firmware version and makes the device eligible to receive released
product firmwares once again.

To unlock a device, visit the device's details view by clicking on it
from your product's device list. Click the **Edit button** (shown
above), and then click the **Unlock** button:

<img class="full-width" alt="Unlock device firmware"
src="/assets/images/unlock-firmware.png" />

The device above is now unlocked from version 3 of product firmware, and
may be targeted to receive a released firmware next time it handshakes
with the cloud.

#### Firmware Precedence Rules

Devices in your fleet will be targeted to
receive a version of product firmware according to these precedence
rules:

- A device that has been **individually locked** to a version of product
firmware is respected above all else, and will not be overwritten by any
released firmwares.

- If unlocked, devices **belonging to a group** will receive the
corresponding group's released firmware (if a firmware has been released
to the group). When a device belongs to multiple groups that each have
released firmware, the _highest firmware version_ will be preferred

- If a device is unlocked and **does not belong to any groups** with
released firmware, it will receive the **Product default** released
firmware (if a firmware has been released as the Product default)

- If none of the above conditions result in a device being targeted for
a product firmware, it will not receive an automatic OTA update from the
Particle cloud

### Managing Customers

Now that you have set up a Product, your customers will be able to create accounts on the Particle platform that are registered to your Product. When properly implemented, your customers will have no idea that Particle is behind the scenes; they will feel like they are creating an account with *ACME, Inc.*.

There are three ways you can authenticate your customers:

- **Simple authentication**. Your customers will create an account with Particle that is registered to your product. You do not need to set up your own authentication system, and will hit the Particle API directly.
- **Two-legged authentication**. Your customers will create an account on your servers using your own authentication system, and your web servers will create an account with Particle for each customer that is paired to that customer. Your servers will request a scoped access token for each customer to interact with their device. This is a completely white-labeled solution.
- **Login with Particle**. Your customers will create a Particle account and a separate account on your website, and link the two together using OAuth 2.0. Unlike the other authentication options, this option will showcase Particle branding. This is most useful when the customer is aware of Particle and may be using Particle's development tools with the product.

As customers are created for your product, they will begin to appear on your Customers (<i class="ion-user"></i>) page. For each customer, you will be able to see their username and associated device ID. Note that the device ID column will not be populated until the customer goes through the claiming process with their device. Customers are commonly used for Wi-Fi products because you will often need a mobile app to configure Wi-Fi network credentials. Creating a customer associates a user with their device or devices, and allows a mobile app to communicate directly with the Particle cloud API on behalf of only that user.

For cellular devices, you can use customer accounts as well. However, it is common to use two other methods:

Single account claiming claims all devices to a single account owned by the product creator. Cellular apps often use a web app, which does not need to have Particle API access per-user. Instead, they can handle this in the back-end. Even cellular products that have a mobile app may prefer to implement them using a mobile framework and communicate from the app to their own back-end using standard web technologies instead of the Particle API. This makes it easier to find app developers, since they don't need to know about the Particle platform.

Unclaimed product devices eliminate the claiming step entirely. This simplifies device setup. However, there is an important limitation: unclaimed product devices cannot subscribe to events. They can, however, receive OTA updates, and handle Particle functions and variables. The Asset Tracker Tracker Edge firmware typically operates using unclaimed product devices.


### Monitoring Event Logs

The Logs page (<i class="icon-terminal"></i>) is also available to product creators! Featuring the same interface as what you are used to with the [developer version of the Console](/tutorials/device-cloud/console/), the logs will now include events from any device identifying as your product. Use this page to get a real-time look into what is happening with your devices. In order to take full advantage of the Logs page, be sure to use `Particle.publish()` in your firmware.

### Managing your billing

To see all billing related information, you can click on the billing icon in the sidebar (<i class="ion-card"></i>). This is the hub for all billing-related information and actions. For more specifics about the pricing tiers and frequently asked questions, [go check out the Pricing page](https://www.particle.io/pricing).

### How billing works

#### Free tier

- Up to {{freeTierDevices}} devices, any mix of cellular and Wi-Fi
- {{freeTierDataOperationsUnit}} Data Operations ({{freeTierDataOperationsComma}}) per month, for both cellular and Wi-Fi, pooled across all devices
- Up to {{freeTierDataOperationsCellularData}} of cellular data per month, pooled across all devices, at no charge
- No credit card required
- Device communication is paused<sup>1</sup> when the monthly limit is reached

For more information see [Device Cloud - Introduction - Pricing](/tutorials/device-cloud/introduction/#pricing).

<sup>1</sup>During the transition period, a warning will be sent but communication will not be immediately paused.

#### Free tier products

Products can be prototyped in the Free tier at no charge. However, there is a limit of {{freeTierDevices}} devices for Free tier products. 

#### Growth tier

- A block includes {{growthTierDataOperationsUnit}} Data Operations ({{growthTierDataOperationsComma}}) per month and up to {{growthTierDevices}} devices
- Add as many blocks as you need for more Data Operations or more devices
- No limit to the number of blocks you can purchase self-service
- Up to {{growthTierDataOperationsCellularData}} of cellular data per month ({{growthTierDataOperationsTrackerData}} for Tracker), pooled across all devices, for each block purchased
- Email support
- Available in Summer 2021

In the Growth tier, usage is measured by blocks. You can choose how many blocks you initially want to purchase in advance. It is also possible to add blocks if you run out of Data Operations, available devices, or cellular data.

In the Growth and Enterprise tiers, you will also have access to an **Organization**, which allows finer access control to multiple products. 

The number of devices is limited by the number of blocks you have purchased, 100 devices per block. You can purchase as many blocks as necessary to support number of devices you need.


### Status
It’s easy to find out the status of your Product’s metrics. Visit [console.particle.io/billing](https://console.particle.io/billing) and you’ll see an up-to-date list of each Product you own, how many outbound events they’ve used that billing cycle, number of devices in each, and how many team members they have. The renewal date for each Product plan is also shown, so you know when the next bill is coming up.

### Updating your credit card

You can update your credit card from the billing page by clicking on the "UPDATE" button next to the credit card on file. Whenever your credit card on file expires or no longer is valid, be sure to update your credit card info here to avoid any disruptions in your service.

### Failed Payments

If we attempt to charge your credit card and it fails, we do not immediately prevent you or your team from accessing your Device Management Console. We will continue to retry charging your card once every few days <strong>for a maximum of 3 retries</strong>. You will receive an email notification each time an attempt is made and fails. When you receive this notification, the best thing to avoid any interruption in service is to <a href="#updating-your-credit-card">update your credit card</a>.


## Asset Tracker Features

All Asset Tracker devices are intended to be used in a product, not as developer devices. This makes it easy to manage a fleet of asset trackers, allowing per-fleet and per-device configuration settings, and features like fleet mapping. The Product Features in the previous section also apply to Tracker devices.

### Create Product

When you create a product with **Asset Tracker (Cellular** as the type, the Asset Tracker features are enabled for the product. Even if you have an existing product, you'll need to create a new Asset Tracker product as products can only have  a single type of device. For example, a product cannot have both an Asset Tracker and a Boron in it. This is done automatically for you if you use [setup.particle.io](https://setup.particle.io).

![Create Product](/assets/images/tracker/create-product.png)

It's OK if you're starting out with a single Tracker; you can create a free prototyping level product that only has one device in it.

### Map

![Map View](/assets/images/tracker/map-view.png)

The map view shows your fleet of devices or selected devices on a map. The Map view is available for Asset Tracker products in the **Maps** icon.

![Map Icon](/assets/images/tracker/map-icon.png)

You can show a subset of your devices on the map by searching:

- By Device ID
- By Device Name
- By [Device Groups](/tutorials/product-tools/device-groups/)

You can also search by the last known location, or within a certain time range.

![Map Search](/assets/images/tracker/map-search.png)

And view details about a specific device:

![Details](/assets/images/tracker/details.png)

On the Tracker One the temperature ("temp") is shown in degrees Celsius. This is the temperature on the board, within the enclosure, and will typically be several degrees warmer than the ambient temperature.

### Device Fleet Settings

Your Tracker devices can be configured fleet-wide, or by device. The fleet-wide settings are in the **Map View**. Click **Gear** icon in the upper-left corner of the map to update Tracker Settings.

![Settings Icon](/assets/images/tracker/map-settings.png)

Note that the settings are automatically synchronized with the device, even if the device is asleep or disconnected at the time the change is made. When the device connects to the cloud again, the checksum of the current device and cloud settings are compared, and if they are different, an updated configuration is sent to the device.

#### Location Settings

![Location Settings](/assets/images/tracker/settings-1.png)

The Location settings include:

- **Radius Trigger** in meters, floating point. When the current position's distance from the last publish exceeds this distance, the new position is published. 0.0 means do not use a publish radius. The GNSS is not monitored during sleep mode, and the radius will only be checked when otherwise waking from sleep. The maximum location update frequency still limits how frequently publishes occur even if if the radius trigger is reached.

| US Units | Meters |
| :--- | :--- |
| 1 yard (3 feet) | 0.91 meters (approximately 1 meter) |
| 100 feet | 30.5 meters |
| 100 yards (length of American football field) | 91.4 meters |
| 1/4 mile | 402 meters |
| 1/2 mile | 805 meters |
| 1 mile | 1609 meters |

- **Maximum location update frequency** in seconds. Wait at least this long in seconds after the last location publish before publishing again. 0 means do not limit. The maximum location update frequency prevents publishing too frequently, which can use excessive amounts of data. 

  When using sleep modes, this also controls how often to connect to the cellular network. A maximum location update frequency value of 10 minutes (600 seconds) or larger is recommended. Setting a very short maximum location update frequency with sleep mode can cause your SIM card to be banned for excessive reconnection to the cellular network by your mobile carrier. 

- **Minimum location update frequency** in seconds. Publish location this often (in seconds) even if there is no movement or other wake trigger. 0 means do not use an minimum update frequency; only publish location information when there is another trigger, such as movement. Including a minimum location update frequency of 8 hours (28800 seconds) or 24 hours (86400) can be helpful to make sure the device is still responding and report its battery level.

In some cases, you will want to set the maximum and minimum to the same value. This is common if you are not using a trigger like movement and instead always want to publish at a fixed frequency.

| Common Unit | Seconds |
| :--- | ---: |
| 1 minute | 60 |
| 5 minutes | 300 |
| 10 minutes | 600 |
| 15 minutes | 900 |
| 30 minutes | 1800 |
| 1 hour | 3600 |
| 2 hours | 7200 |
| 4 hours | 14400 |
| 8 hours | 28800 |
| 24 hours | 86400 |


- **Minimize Data**. If checked, only only latitude and longitude data is sent on each location publish. If unchecked (the default), additional information such as speed and heading are sent.

- **Publish on GPS lock**. If checked, publish location when GNSS lock is obtained, even if the device has not reached the radius trigger or maximum location update frequency yet. The minimum location update frequency is still obeyed.

- **Acknowledge location publishes**. If checked, the device will expect cloud acknowledgement of location publishes and retry failed transmissions. If unchecked, one attempt will be made to send, which may or may not succeed. If you are publishing frequently, it may be preferable to lose some points, rather than record delayed information.

- **Enhanced location**. If checked, the Particle cloud will process location fusion, enhanced geolocation using Wi-Fi access points and cellular tower information.

- **Publish cellular tower data**. If checked, the Tracker will include information about nearby cellular towers with location events.

- **Publish GNSS data**. If checked, the Tracker will use the GNSS (GPS) module for geolocation.

- **Publish Wi-Fi access point data**. If checked, the Tracker will include nearby Wi-Fi access points in location publishes. The Wi-Fi access points are not connected to; most Wi-Fi access points periodically broadcast their presence to allow Wi-Fi devices to find them. This public information is used by the Wi-Fi geolocation service.

- **Callback to device with enhanced location data**. If checked, the Particle cloud will send back enhanced geolocation data obtained from Wi-Fi or cellular tower information back to the device. This is useful if your device firmware wants to process this information on device. If you're only tracking location from the cloud, it's not necessary to enable this option.


#### Motion Settings

![Motion Settings](/assets/images/tracker/settings-2.png)

The motion settings determine how the IMU (inertial measurement unit, the accelerometer) is used to determine whether to publish a location. The **Interval minimum** also applies to motion events. Movement events can occur while the device is awake, also also wake a device from sleep mode.

- **Movement** publishes if the device moves, and has several sensitivity options:

  - **Disable**: Do not use motion detection (the default).
  - **Low**: Least sensitive, large motion is required to publish.
  - **Medium**
  - **High**: Most sensitive, even a small amount of motion will trigger publish.

- **High G** publishes if there is a High-G acceleration event, such as the device falling. This is 4g for at least 2.5ms.

  - **Disable**: High-G events are not generated (the default).
  - **Enable**: High-G events are generated.


#### RGB LED Settings

![RGB LED Settings](/assets/images/tracker/settings-4.png)

The Tracker Firmware configures the RGB status LED. 

The **Type** popup menu has the following options:

- **off**: The RGB LED is turned off (dark).
- **tracker**: Color indicates signal strength (yellow = lower signal strength, green = higher signal strength). Fast breathing red while connecting to cellular.
- **particle**: Use standard Particle colors like breathing cyan instead of tracker-style colors. Default for Tracker SoM Evaluation Board.

#### Sleep Settings

![Sleep Settings](/assets/images/tracker/settings-5.png)

Sleep mode allows the device to enter a low-power state when idle, conserving battery power. Sleep requires Tracker Edge v10 and Device OS 2.0.0-rc.3 or later. There are additional details in the [Tracker Sleep](/tutorials/asset-tracking/tracker-sleep/) page.

**Sleep Mode** can be set to **enable** or **disable**. 

**Post Publish Execution Time** is the minimum duration in seconds to stay awake after publishing before going to sleep. The default is 10 seconds. This provides enough time to make sure a software update can be started when waking up from sleep.

**Maximum Connecting Time** is the maximum duration, in seconds, to wait for being cellular-connected and to obtain a GNSS lock before publishing. If connecting takes too long, then the device will go back to sleep instead of continuously attempting to connect. The default is 90 seconds.

You can find out more in the [Tracker Sleep Tutorial](/tutorials/asset-tracking/tracker-sleep/).

#### Typical Settings

Typical settings in common scenarios:

**Vehicle (detailed information)**

  - Radius Trigger: 151 meters (500 feet)
  - Maximum location update frequency: 30 seconds
  - Minimum location update frequency: 900 seconds (15 minutes)
  - Sleep: disabled

  This will get detailed location information, but limits the data to at most once every 30 seconds. If the vehicle is moving 24 hours a day you will exceed your 25 MB data quota, but as long as it's in movement less than half of the time you'll be within the limit. The minimum location update frequency assures that events will be published periodically when stationary, so the cellular signal and battery strength will be known.

**Vehicle (less detail)**

  - Radius Trigger: 1600 meters (1 mile)
  - Maximum location update frequency: 300 seconds (5 minutes)
  - Minimum location update frequency: 900 seconds (15 minutes)
  - Sleep: disabled

  This will provide an approximate location while using less data, for example if you are looking for the general area of the vehicle. The minimum location update frequency assures that events will be published periodically when stationary, so the cellular signal and battery strength will be known.

**Tracking an item for location and theft prevention with external power**

  - Movement: Medium
  - Maximum location update frequency: 30 seconds
  - Minimum location update frequency: 3600 seconds (1 hour)
  - Sleep: disabled
  
  If the item is moving, the location will be published every 30 seconds. This should not be used if the item will be in movement 24 hours a day, as you will exceed the 25 MB data limit. However, if it's typically not moving this will be fine. It also updates the location information every hour even when not moving.

**Tracking an item - battery only**

  - Movement: Medium
  - Maximum location update frequency: 900 seconds (15 minutes)
  - Minimum location update frequency: 28800 seconds (8 hours)
  - Sleep: enabled
  
  If the item is moving, the location will be published every 15 minutes, otherwise the device will be in sleep mode to conserve battery power. It will also update location every 8 hours even when not moving. More sleep-related examples can be found in the [Tracker Sleep Tutorial](/tutorials/asset-tracking/tracker-sleep/#common-scenarios).

**Periodically sending information**

  - Maximum location update frequency: 120 seconds (2 minutes)
  - Minimum location update frequency: 120 seconds (2 minutes)
  - Sleep: disabled

  If you have additional sensors that you are monitoring, and you want to continuously send samples at set time intervals, just set the maximum.


#### Data Usage

The location publish will vary in size depending on the trigger reason(s) and other factors, but this is a rough guideline.

This is a typical location publish you can see in the console. It is 209 bytes. 

```json
{"cmd":"loc","time":1596043291,"loc":{"lck":1,"time":1596043291,"lat":42.46973211,"lon":-75.06480125,"alt":322.294,"hd":214.60,"h_acc":10.000,"v_acc":16.000,"cell":40.2,"batt":99.6},"trig":["time"],"req_id":3}
```

The actual overhead is:

- 209 Location publish payload
-  40 Location publish overhead
- 231 Event confirmation and other acknowledgements

For the purposes of our calculations and to leave a bit of room for other data fields that might be present we'll assume 500 bytes per location publish.

If you're adding custom data to the publish, measure the size of your total payload as viewed in the console, then add 271 bytes (40 + 231) to see how much data your larger publish will use.

For time trigger, here are some general guidelines. These are just location publishes and do not include overhead such as connecting to the cloud, firmware updates, etc..

| Time Interval | Data Usage Per Month |
| :------------ | :------------------- |
| 1 minute      |   20 MB |
| 5 minute      |    4 MB |
| 1 hour        |  351 KB |
| 1 day         |   15 KB |

(Assumes 30 days in a month on average.)


### Device Settings

Normally, you will use the product settings across your fleet of Tracker devices. If you mark a device as a Development Device, you can change settings on a per-device basis within the Device Configuration.

![Per-Device Settings](/assets/images/tracker/per-device.png)

### View Device

#### Using the cmd box

When viewing a device in the console, in the functions and variables area on the right, is the **cmd** box.

<div align=center><img src="/assets/images/tracker/tracker-enter-shipping.png" class="small"></div>

Some commands you can enter into the box:

| Command | Purpose |
| :------ | :--- |
| `{"cmd":"enter_shipping"}` | Enter shipping mode |
| `{"cmd":"get_loc"}` | Gets the location now (regardless of settings) |
| `{"cmd":"reset"}` | Gracefully reset the device (Tracker Edge v13 and later) |

Shipping mode powers off the device by disconnecting the battery. This allows a Tracker One to be shipped in a way that the battery does not discharge without having to open the case and disconnect the battery. Note that you can only get out of shipping mode by connecting the device to USB power or power by the M8 connector. It works on the Tracker SoM evaluation board, but is less useful there since it has physical power switches.

It's also possible to [create custom `cmd` handlers](/reference/asset-tracking/tracker-edge-firmware/#regcommandcallback-cloudservice). These can be used instead of creating a custom Particle function handler and make it possible to add more than 12 handlers and automatically decode JSON arguments to the cmd handler.

On a successful cmd request, the result is 0. A result of -22 indicates the JSON is invalid. 

**Warning:** Particle has discovered an issue with GPIO current leakage through Tracker One's M8 connector that affects Tracker One v1.0 devices manufactured prior to August 31, 2020 and can adversely affect the use of shipping mode for devices that use the M8 connection to an external peripheral device. For more information see [TAN002 - Tracker One v1.0 Shipping Mode](https://support.particle.io/hc/en-us/articles/360052713714).

### Using off-the-shelf releases

To use off-the-shelf Tracker Edge firmware releases, click on the **Firmware** icon in your product in the console.

![Releases](/assets/images/tracker/release.png)

Instead of having to manually upload firmware that you write, by default new releases are automatically added to your firmware list. Just click the **Release Firmware** link to release a new version to your fleet.

Once you've uploaded custom firmware to your product, the off-the-shelf releases will no longer be added automatically.
