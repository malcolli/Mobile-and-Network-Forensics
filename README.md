# Mobile-and-Network-Forensics
Project of the Forensics Process of Mobile and Network Forensics and Cyber-Crime Scene Analysis

# Purpose
The various laws and regulations dealing with computer forensic analysis will be discussed. 
We will analyze and synthesize the collection, preservation, analysis, and presentation 
of mobile and network evidence. Acting as a Forensics Analyst, we will analyze evidence 
to the emerging international standards for computer forensic analysis, as well as a formal 
methodology for conducting mobile and digital forensic investigations.

**Digital Forensics Report– SK8000PUA 55’’ 4K HDR Smart LED SUPER UHD TV**

```
By Malcolm Collins and Blaine Milburn
```
```
Date: March 13th, 2023
```
```
Dr. Connie Justice
```

## Table of Contents


- Executive Summary .................................................................................................................
- Overview.................................................................................................................................
- Case ........................................................................................................................................
- Objectives ...............................................................................................................................
- Evidence ..................................................................................................................................
   - Introduction......................................................................................................................................
   - Table 1: Evidence Record ..................................................................................................................
- Analysis...................................................................................................................................
   - Statement of Professional Responsibility ..........................................................................................
   - Tools.................................................................................................................................................
   - Narrative ..........................................................................................................................................
      - Evidence Integrity Verification and Working Dataset Generation .....................................................................
      - Evidence Drive Hash Integrity Verification ..........................................................................................................
      - Generating Working Dataset .............................................................................................................................
      - Working Data Ingest into Autopsy Forensic Examiner .....................................................................................
      - Evidence of Counter Forensics Techniques ........................................................................................................
      - File Carving and Keywords Search .....................................................................................................................
      - Sanitization of Working Dataset Data ..............................................................................................................
- Relevant Findings ..................................................................................................................
   - Objective 1 – Evidence of Accusations.............................................................................................
      - Connected Device Log ........................................................................................................................................
      - USB Device Temporary Storage .........................................................................................................................
      - USB Device Storage Manifest ............................................................................................................................
      - Song File .............................................................................................................................................................
   - Objective 2 – Evidence of Ownership ..............................................................................................
      - INI Configuration Files ........................................................................................................................................
   - Objective 3 - Evidence of Counter Forensics Techniques..................................................................
      - Disk Formatting ..................................................................................................................................................
   - Objective 4 – Preservation of Evidence Integrity .............................................................................
      - Disk Image Integrity ...........................................................................................................................................
      - Integrity of Identified Artifacts of Interest ........................................................................................................
- Conclusion and Recommendations ........................................................................................
   - Conclusion ......................................................................................................................................
   - Recommendations ..........................................................................................................................
- References.............................................................................................................................


## Executive Summary 

OctoForensics was contracted by Densborn Blachly LLP to complete a digital forensic
investigation of an LG SK8000 55” smart TV on the behalf of their plaintiff, Connie Justice, who alleged
that the defendant, Clay Hampton, engaged in copyright infringement against her prominent TV show.
Upon receipt of the evidence from the Indianapolis Police Department, OctoForensics performed a
forensically sound investigation of the onboard storage from the smart TV using industry standard tools
and discovered evidence of a removable media drive that may have contained the subject of the
copyright infringement allegation, and should be the focus of further investigation. Furthermore,
OctoForensics discovered direct evidence of copyright infringement in the form of an MP3 music file
that contained the theme song for the plaintiff’s intellectual property. Lastly, OctoForensics identified
that the smart TV had been quick-formatted and been left unused afterwards, which is indicative of
potential counter-forensics activity. Upon conclusion of the forensic investigation, all evidence was
returned to the Indianapolis Police Department and local working copies of the evidence were
destroyed according to the Department of Defense 5220.22-M standard.


## Overview

As explained by the United States Copyright Office, copyright law was birthed into the United States
Constitution in Article I, Section 8 in the year 1790 (United States Copyright Office, 2023). To elaborate,
Article I, Section 8 of the United States Constitution states, “Congress shall have the Power to promote
the Progress of Science and useful Arts, by securing for limited Times to Authors and Inventors the
exclusive Right to their respective Writings and Discoveries.” Moving to modern jurisprudence, the
United States Copyright Office defines that copyright law, and its applicable sanctions are now enforced
through the Copyright Act of 1976, signed by President Gerald Ford.

Any artistic work whose owner desires to protect under current copyright laws must first register the
work with United States copyright office (Stim, 2023). Once registered, the work is then legally
protected from unauthorized reproduction, distribution, performance, display, or used as a basis for
derivative work (United States Copyright Office, 2023). If a copyright holder recognizes a violation of
their copyright by a third-party, the copyright holder is entitled to civil action to reclaim damages.

Modern smart televisions are essentially computers that are not so different from your typical tablet
computing device. As described by LG’s product page for the 55-inch SK8000PUA Smart TV, this model
utilizes the LG WebOS operating system (LG, Inc., 2023). LG WebOS is a Linux-based operating system
tailored for use in smart televisions that was developed by HP as Open WebOS and later sold to LG
under its current name, “LG WebOS” (Gupta, 2013). Specifically, LG WebOS maintains a lot of the typical
functionality that one can expect from a typical Linux-based operating system such as file system
structure, networking operations, etc.

As for the physical design, the LG SK8000PUA Smart TV contains and runs its LG WebOS system on a
custom, small form factor motherboard located on the back side of the television panel. Within the
motherboard, the onboard memory that contains the operating system image is a soldered embedded
multimedia card (eMMC) storage device (ElectroParts, 2023). Thus, to capture the storage media
contained on the LG SK8000PUA Smart TV, OctoForensics will de-solder the onboard eMMC storage
device and connect it to our purpose-built eMMC data acquisition unit in read-only mode.

Once connected, our data acquisition device will create a bit-for-bit disk image of the eMMC storage
module and provide us with the SHA1 and SHA256 hash values of the original disk image and the copied
disk image for verification. After completion of the data acquisition stage, the eMMC storage module
will be removed from the data acquisition device and stored in a sealed static-proof bag until needed by
the applicable parties as approved by the officiating judge at trial.

Moving onto the analysis of the captured image of the eMMC storage device, our team will utilize the
Autopsy forensic toolkit to perform an analysis of the storage device and identify any potential
interesting artifacts from the image. Following this brief identification phase, our forensic investigators
will pivot to conducting a full forensic investigation of the captured image in furtherance of completing
our objectives defined on page 5.


## Case

On March 13th, 2023, OctoForensics group was contracted by Densborn Blachly LLP to perform forensic
analysis on an LG SK8000PUA 55” Smart TV on behalf of the plaintiff they represent in a copyright suit,
Dr. Connie Justice. The defendant, Clay Hampton, is accused by Dr. Justice of consuming her copyrighted
digital media titled, “My Little Pony – Cybersecurity is Magic” without prior authorization or licensure.
Thus, Densborn Blachly LLP charged OctoForensics with analyzing the defendant’s LG SK8000PUA 55”
Smart TV, which was obtained during the discovery phase of the civil suit.

On March 15th, 2023, OctoForensics group became in possession of the defendant’s LG SK8000PUA 55”
Smart TV. This evidence was obtained by forensic examiner, Malcolm Collins from the Monroe County
district court’s evidence clerk, Marcy Jackson at 8:02AM. Upon receipt, Malcolm Collins transported the
evidence directly to the OctoForensics evidence room at 8:37AM and properly filed the chain of custody
documentation found in Appendix A.

## Objectives

The objective of this forensic investigation is to examine the evidence provided by the
Densborn Blachly LLP on behalf of the plaintiff, Dr. Connie Justice, for evidence of copyright
infringement based on the Copyright Act of 1976 perpetrated by the defendant, Clay Hampton.
OctoForensics will endeavor to conduct a complete forensic investigation of the evidence at
hand and provide an empirical analysis of all findings in accordance with the court’s warrant
and its subsequent limitations. Specifically, OctoForensics will conduct a forensic analysis to:

1. Determine if the evidence provided contains any further evidence confirming or refuting
any violations of the Copyright Act of 1976 from the defendant’s side.

2. Confirm that the device in question does indeed belong to the defendant through
obtaining any evidence of ownership from the device.

3. Identify any potential counter forensic techniques that would qualify as destruction of
evidence.

4. Prove and maintain the forensic integrity of the evidence provided by the courts upon
receipt.


## Evidence 

Will include in this PDF download

## Introduction

Essential in adhering to legal requirements, evidence should be stored in a manner that preserves its
integrity and protects it from damage, tampering or other compromising scenarios (Matheson, 2015).
Following protocol for storing the evidence, the television goes through extensive lengths to get
properly handled. The television is properly packaged, then labeled and documented. Proper packaging
makes sure the physical and digital evidence (hashed data) is preserved and not compromised. Hashed
data is mapped input data that is arbitrary to a fixed-length value and then converts an encrypted
output (usually called a digest). This function of hashing data makes them useful for security purposes
by making sure threat actors who can gain access to the stored hash values cannot retrieve the original
data. While hashed data can’t be used to “reverse-engineer” the input, having any tampering or changes
would be considered compromising to the case and its validity (National Institute of Standards and
Technology, 2023).

### Table 1: Evidence Record ..................................................................................................................

Will include and upload from PDFl

## Analysis

## Statement of Professional Responsibility 

As practitioners in the field of digital forensics, it is my responsibility to provide an accurate, unbiased,
and professional analysis of the evidence provided for the case in hand. At no point will I draw
conclusions or postulations beyond the scope of the expertise I am charged with providing. If at any
point our expert testimony were to change, it is our duty to report it to all parties involved immediately
upon recognition.

## Tools

The tools utilized in this forensic investigation are as follows:

####  Forensic Toolkit (FTK) Imager

```
Forensic Toolkit (FTK) Imager is a digital forensics software suite that allows a user to import, create,
clone, and examine disk images (Exterro, Inc., 2023). In this case we will be leveraging FTK Imager to
import the forensic evidence contained on a thumb drive provided to us by the court via the
discovery process. After importing the original evidence, our team will then create a one-for-one
clone of the original evidence image using FTK Imager’s cloning capability. At the beginning, middle,
and end of every step, our team will collect a forensic signature for both images, as relevant, to
ensure that the integrity of the original evidence image and the clone image are unchanged from
their original states.
```
####  Autopsy Digital Forensics Platform – Ver. 4.20.

```
Autopsy Digital Forensics is a software platform that is utilized to collect, organize, and identify
contents of an electronic storage medium in a forensically sound manner (BasisTech, 2023).
Furthermore, Autopsy provides the capability to audit data authenticity with real-time hashing. Thus,
in this case, our team will be utilizing Autopsy Digital Forensics to conduct the actual examination
portion of the forensic process. In addition, Autopsy will be monitoring the image cloned from the
original evidence to ensure that it remains an exact copy that is forensically sound.
```
####  Windows 11 Professional Operating System – Ver. 22H

```
Operating System that provides the capability to interact with and manage digital evidence and
forensic tools. This device is not connected to the internet and is used as a secure, standalone
analysis platform. Upon request, the setup parameters and software inventory of this device can be
provided.
```
####  Tableau TK8 Forensic USB 3.0 Bridge

```
The Tableau TK8 Forensic USB 3.0 Bridge is a piece of hardware that you plug a USB storage device
into to ensure that when connected to your computer, no writing operations can occur against the
USB drive. To elaborate, if you directly connect a USB device to a computer system, you run the risk
of changing the data in even the most infinitesimal of ways. If this were to occur during a forensic
investigation, the evidence’s integrity would be ruined and be rendered inadmissible in court. Thus,
by using this Tableau TK8, our team can ensure that the computer has no capability to change or
corrupt the evidence stored within the provided USB drive.
```

### Narrative ..........................................................................................................................................

#### Evidence Integrity Verification and Working Dataset Generation .....................................................................

As required by protocol, OctoForensic’s examiners will never perform direct analysis on the original
evidence item. Instead, the examiner will verify the integrity of the evidence, generate a clone of the
evidence that is scientifically verified, and finally verify the integrity of the evidence one final time
before returning it to safe custodianship. Then, the forensic examiner will conduct analysis on that
cloned dataset that is scientifically verified to be an exact copy of the original evidence. This exact copy
of the evidence is referred to as the working dataset. This procedure ensures the integrity of the original
evidence without running the risk of accidentally corrupting the authenticity of the original evidence
item during the analysis phase of our forensic investigation.

#### Evidence Drive Hash Integrity Verification ..........................................................................................................

To begin creating the working dataset of the LG SK8000PUA TV storage medium, Blaine Milburn
(examiner) checked out the digital disk image ( **Evidence ID: 003** ) from the evidence manager, Malcolm
Collins on April 1, 2023, at 3:14PM EST. Upon collection of the digital disk image, the examiner
completed their entry on the chain of custody documentation and moved the evidence item to the
forensic laboratory for analysis. Before conducting any analysis on the disk image at hand, the examiner
connected the USB drive containing the original evidence image to the Tableau TK8 forensic USB 3.
bridge and imported the evidence image into FTK Image. With the image imported into FTK Imager, the
forensic investigator immediately conducted a hash signature verification against the evidence image.
This verification confirmed the integrity of the evidence image by returning the following values shown
below in figure one:

Evidence Drive Hash Values – April 1, 2023, at 3:28PM EST.

####  MD5: a915aa103547d580dbdf4cb3d30a7a5f

####  SHA1: 6f923a094f2bf1d3efc6dbef0ff6d

```
Figure 1: Importing and Verifying Evidence Integrity using FTK Imager
```

#### Generating Working Dataset .............................................................................................................................

With the original evidence’s forensic integrity confirmed, the forensic examiner began to clone the
evidence image to the forensic workstation using FTK Imager. Shown below in figure two, you can see
the completion report of this clone operation which includes a final verification of the original evidence
image as well.

Evidence Drive Hash Values – April 1, 2023, at 3:34PM EST.

####  MD5: a915aa103547d580dbdf4cb3d30a7a5f

####  SHA1: 6f923a094f2bf1d3efc6dbef0ff6d

Working Dataset Hash Values – April 1, 2023, at 3:34PM EST.

####  MD5: a915aa103547d580dbdf4cb3d30a7a5f

####  SHA1: 6f923a094f2bf1d3efc6dbef0ff6d

```
Figure 2: Evidence Image Cloning and Verification Using FTK Imager
```

With the evidence successfully verified to be intact and secured on the Windows 11 forensic workstation,
the examiner then updated the chain of custody documentation and returned the USB drive containing
the original evidence image ( **Evidence ID: 003** ) to the evidence manager, Malcolm Collins for storage.

#### Working Data Ingest into Autopsy Forensic Examiner .....................................................................................

With the hash signature verified to still be unaltered, the examiner then began running the evidence
ingest modules on the working dataset. To elaborate, Autopsy is specifically tailored to disk image
forensics and separates its functionality into “modules.” These modules provide a variety of automated
analysis tasks such as looking for emails, determining the last time certain files were used, etc. It is
OctoForensic’s policy to always run all standard Autopsy modules on any disk image they are charged
with analyzing. As a reminder, once a disk image has been imported into Autopsy, it will maintain a
constant watch over the image’s hash signature and alert at any time the forensic integrity has been
violated.

```
Figure 3: Autopsy Ingest of Working Dataset Image
```
#### Evidence of Counter Forensics Techniques ........................................................................................................

After the completion of the Autopsy ingest modules, it became apparent to the examiner that this
device had been attempted to be wiped prior to being brought into the court’s custody. To explain, all
digital storage mediums used in modern computing rely on the usage of a file system. A file system is
comparable to a filing cabinet that contains drawers for storing files in. Although a computer file system
is a bit more complex, in essence, it provides an organized way for the computer system to store and
read data on a storage device.

This talk of file systems is brought up because although a file system was found on the disk image, it had
no files cataloged in it. In the world of digital forensics, this means that someone conducted a format
operation on the storage device. Again, to explain, formatting a storage device simply means removing
the “filing cabinet” from the computer system and putting a new, empty filing cabinet in. However,
there are two types of format operations.

The first operation is a quick format. Relating back to our filing cabinet analogy, a quick format would be
akin to taking all the files out of the filing cabinet, leaving them on the floor and putting a new filing
cabinet in the room. That is, the files are still within the storage device, but the file system does not
have an official record of them for the computer system to know that they exist (EaseUS , 2023). The
second operation is called a slow or full format. Back to the analogy, a full format would be akin to


removing the old filing cabinet and burning all the old files. Specifically, during a full format, the
computer system will completely reset the storage medium by ensuring no data is stored on it, and then
install the new file system for the computer system to use, in a like-brand-new state.

In digital forensics, any activity performed to make the recovery of evidence more difficult is referred to
as “counter forensics.” In this instance, the evidence in this case had a quick format performed on it.
This is definitively provable because although the device had a file system on it with no files officially
registered to it, Autopsy found 5638 files stored on the disk image outside of the file system. The
process of finding these files that exist outside of the file system is called file carving (Infosec Institute,
Inc., 2018). Shown below in figure four, you can see that this image has no known files associated with
its file system by observing the Deleted Files option located along the left-hand side.

```
Figure 4:Evidence of Counter Forensic's - Disk Formatting
```

#### File Carving and Keywords Search .....................................................................................................................

Luckily, although a disk format was likely attempted on this device, Autopsy automatically performs a
file carving process to capture and recover any residual data residing on the image, but not contained in
the file system. In total, Autopsy was able to identify 5638 total files that were existing outside of the file
system. However, going line by line through each file is not a practical solution. Instead, it is the practice
of any seasoned forensic examiner to execute a keyword search to identify potential files of interest. In
this case, shown below in figure five, you can see the keyword list utilized within Autopsy to identify
potential pieces of evidence. To explain, each of these keywords were generated in coordination with
the hiring law firm and were based on the facts of the case.

```
Figure 5: Keyword List
```

Upon completion of the key word’s search, the forensic examiner began the process of reviewing the
findings for anything that was deemed relevant to the objectives outlined in objective’s section of this
forensic report. Accordingly, all relevant findings will be provided in the relevant findings portion of the
report below.

```
Figure 6: Evidence Keyword Search Results
```
#### Sanitization of Working Dataset Data ..............................................................................................................

Lastly, upon conclusion of the working dataset analysis, the forensic examiner will delete the replicated
disk image from the forensic workstation and initiate a device storage wipe. This storage wipe follows
the Department of Defense (DoD) standard of three full disk wipes (Mehta, 2022). Concisely, this
process ensures no one can collect previously examined forensic data and that all forensic examinations
are conducted using a sterile computing environment free from latent artifacts.


## Relevant Findings ..................................................................................................................

### Objective 1 – Evidence of Accusations.............................................................................................

#### Connected Device Log ........................................................................................................................................

For background, most computer systems keep a record at all times of any devices that are directly
connected to them. For example, when a user plugs in a new USB drive to a computer, a new record is
created within the computer system that tracks this new USB drive. When creating this record, the USB
drive will provide the computer system with a hardware identification number that is unique to the
drive itself. Thus, if you plug this USB drive into a second computer, you would be able to look at both
computers and determine that at one point in time, both computers had the same USB drive plugged
into them. For more background on USB Device forensics, Kięczkowska has authored an authoritative
guide called “USB Forensics 101,” which provides a myriad of information about USB forensics
(Kięczkowska, 2022).

Accordingly, our examiner was able to find a text log (f0968112.txt) on the TV disk image that contained
a record of all devices plugged into the television at one point in time. Of note within this record is an
entry for a “SanDisk Cruzer Extreme” USB drive with a unique device identifier of
“30303030303030303031314530433433_1.” Bottom line, this finding means that at one point in time, a
USB device labeled “CRUZER EXTREME” was inserted into this television.

```
Figure 7: Removable Storage Connected to TV
```

#### USB Device Temporary Storage .........................................................................................................................

For further background, to provide a faster and more responsive experience for users, some computer
systems will cache data from an external drive on their own local drive. Accordingly, in this forensic
analysis, the examiner found a temporary cache entry related to the previously identified “SanDisk
Cruzer Extreme” USB drive. Specifically, this cache entry contained references to “bunny_movie.mp4.”
This is of note because the plaintiff in this case alleges that the defendant had an unauthorized copy of
their digital video that centered around their new bunny character, “Digit.” Although the video itself is
not within the disk image collected from this television, there is strong evidence that at one point in
time it was at least accessible to it from a SanDisk Cruzer Extreme USB drive.

#### USB Device Storage Manifest ............................................................................................................................

To speed up the process of connecting an external storage device to a computer system, some
computers will create a file that contains a manifest of all the files stored on the external storage device.
In this case, the examiner was able to locate a manifest record that traced back to the “SanDisk Cruzer
Extreme” USB Drive that detailed that among other files, this USB drive contained “bunny_movie.mp4”
and had a recorded file size of 58,252,568 bytes.

```
Figure 8: Evidence of Bunny Movie on External USB Device
```

#### Song File .............................................................................................................................................................

The LG SK8000PUA TV allows users to upload their own favorite song files to the device for playback
later. Accordingly, within this disk image it appears that at one point in time, the user of this device
uploaded a copy of the plaintiff’s copyrighted theme song for the content at dispute to the device. This
file was stored as an MP3 sound file and named “F1113946.mp3.”

```
Figure 9: Identified Song File
```

### Objective 2 – Evidence of Ownership ..............................................................................................

#### INI Configuration Files ........................................................................................................................................

An INI Configuration file is a text file used by software and computer systems to store and read settings
in. For example, if a user wants their desktop background to be purple, there is likely an INI
configuration file stored on their system that says, set the desktop background to purple. Accordingly,
analysis of this disk image unveiled an INI configuration file (f1267416.ini) that stored settings for the
television’s network adapters. Specifically, this television contained one method for connecting to the
local network, one wireless network adapter with a Media Access Control address of 00:51:ED:2B:DB:27.

To explain, a Media Access Control (MAC) Address is used by computers as a way of sending network
traffic from one computer to the next (Yasar, n.d.). Lastly, virtually every computing device that has
networking capability keeps a rolling record of MAC addresses that have recently communicated with it.
Thus, because each device’s MAC address should be unique, the MAC address provides an easy means
of identifying a given device on a network.

These details, while not able to confirm ownership on their own, do provide an easy method for proving
that the defendant may have connected to the device in the past (Rouse, 2016). To explain, the
defendant’s other devices may contain records of connecting to this device’s network adapter. Some
devices of interest to prove this would be the defendant’s phone, router, or personal computer.

```
Figure 10: Wireless Adapter Information
```

### Objective 3 - Evidence of Counter Forensics Techniques..................................................................

#### Disk Formatting ..................................................................................................................................................

As described in the analysis section, after the completion of the Autopsy ingest modules, it became
apparent to the examiner that this device had been attempted to be wiped prior to being brought into
the court’s custody. Specifically, it is beyond certainty that this device had been rendered unusable after
being formatted because no new file system or files exist on this disk image. Thus, someone disk
formatted the device, and left it sitting without use afterwards. Below in figure 11 you can see that no
file system is found on the working dataset image.

```
Figure 11: Autopsy Forensic - Evidence of Disk Formatting
```

### Objective 4 – Preservation of Evidence Integrity .............................................................................

#### Disk Image Integrity ...........................................................................................................................................

At no time during the investigation did the Autopsy forensic investigation platform alert to any evidence
integrity violations. Furthermore, upon completion of the investigation of the working dataset, Autopsy
performed one last hash verification against the disk image and indeed confirmed that the disk image
has remained unchanged by providing the following digital hash signatures:

Autopsy Working Dataset Hash Values – April 2, 2023, at 2:22PM EST.

####  MD5: a915aa103547d580dbdf4cb3d30a7a5f

####  SHA1: 6f923a094f2bf1d3efc6dbef0ff6d

```
Figure 12: Final Verification of Working Dataset
```
#### Integrity of Identified Artifacts of Interest ........................................................................................................

Upon completion of the analysis of the disk image within Autopsy, the examiner exported all relevant
artifacts of interest to a USB drive with hardware encryption enabled and collected a digital hash
signature manifest to easily prove and track their forensic integrity. Furthermore, the examiner created
a new chain of custody documents for this new evidence item and deposited it to the evidence manager,
Malcolm Collins.


## Conclusion and Recommendations ........................................................................................

### Conclusion ......................................................................................................................................

This report provides a detailed record of OctoForensic’s forensic examination of an LG SK8000 55” TV as
contracted by Densborn Blachly LLP and their client, Connie Justice. Specifically, OctoForensic’s was
tasked with identifying any corroborating evidence pertaining to the claim of copyright infringement
against the defendant, Clay Hampton. Using industry standard tools and strict adherence to
OctoForensic’s standard operating procedures (SOP), our forensic examiners were able to identify
potential avenues to prove ownership, detect counter-forensics techniques, provide evidence
corroborating the allegations against the defendant, and maintain and verify the forensic integrity of the
evidence at each step of the analysis procedure. To summarize the key findings of this report, this device
indicates that a USB device was connected to this TV that contained a video labeled “bunny_movie.mp4”
and a song file directly from the subject of the copyright infringement claim.

### Recommendations ..........................................................................................................................

To further the investigation of the claim of copyright infringement, OctoForensics encourages the
plaintiff’s team to check their evidence inventory for any sort of networking devices such as a router or
WI-FI access point to help corroborate ownership of this device to the defendant utilizing the MAC
address provided in the relevant findings section of this report. Moreover, OctoForensics also
encourages the plaintiff’s team to search for a “Sandisk Cruzer” USB removable drive that may contain
the actual digital content at the core of the copyright infringement claim. Lastly, OctoForensics
encourages the plaintiff’s team to ask questions of the defendant under oath pertaining to the potential
counter-forensics techniques identified on the device.


# Exhibits

```
Figure 13: LG SK8000 55'' TV Sales Page. Retrieved from: https://www.lg.com/ca_en/tvs/lg-55SK8000PUA
```
_Figure 14: Tableau TK8 Forensic USB Bridge. Retrieved from: https://security.opentext.com/tableau/hardware/details/t8u_


```
Figure 15: SanDisk Cruzer Line of USB Drives. Retrieved from: https://www.westerndigital.com/brand/sandisk/usb-flash-
drives/cruzer
```
_Figure 16: eMMC Storage Chiplet Example. Retrieved From: https://www.techtarget.com/searchstorage/definition/eMMC-
embedded-MultiMediaCard_


```
Indianapolis Police Department
```
# EVIDENCE CHAIN OF CUSTODY TRACKING FORM

Case Number: _00001234 Offense: Copyright Infringement

Submitting Officer: (Name/ID#) Jethroe Hastings IPD Badge#550_

Victim: _ Dr. Connie Justice

Suspect: _Professor Clay Hampton

Date/Time Seized: March 12, 2023, 13:30

Location of Seizure: Suspect’s Residence

```
Description of Evidence
Item # Quantity Description of Item (Model, Serial #, Condition, Marks, Scratches)
001 1 Television, LG SK8000PUA 55’’, Factory Condition, LG55C431
002 1 Silicon Motion, Inc. eMMC Storage Chip, Undamaged and de-soldered.
Stored in anti-static bag. SN: 1984-SM662GEFBESS-NB
003 1 USB Drive, Kanguru Defender, Contains Forensic image of Item 001.
MD5 Hash: a915aa103547d580dbdf4cb3d30a7a5f
004 1 USB Drive, Kanguru Defender, Contains extracted evidence from
investigation. MD5 Hash: 0df71c69033495c098be36506e6d3dc7
```
```
Chain of Custody
Item # Date/Time Released by
(Signature & ID#)
```
```
Received by
(Signature & ID#)
```
```
Comments/Location
001 2/12/2023
1600
```
```
Jethroe Hastings #550 Patrick Messer #012 IPD Evidence Storage
001 4/13/2023
0800
```
```
Patrick Messer #012 Tim Knowles #010 Collection of Technical
Data
002 4/14/2023
0900
```
```
Tim Knowles #010 Patrick Messer #012 IPD Evidence Storage
003 4/14/2023
0900
```
```
Tim Knowles #010 Patrick Messer #012 IPD Evidence Storage
001 4/14/2023
0900
```
```
Tim Knowles #010 Patrick Messer #012 IPD Evidence Storage
001 4/15/2023
0800
```
```
Patrick Messer #012 Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Transfer to 3rd Party
Forensic Storage
002 4/15/2023
0800
```
```
Patrick Messer #012 Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Transfer to 3rd Party
Forensic Storage
003 4/15/2023
0800
```
```
Patrick Messer #012 Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Transfer to 3rd Party
Forensic Storage
001 4/15/2023 0837 Malcolm Collins – Plaintiff Forensic Investigator Malcolm Collins – Plaintiff Forensic Investigator Stored in Octoforensic’s Evidence Room
```

```
002
```
```
4/15/2023
0837 Malcolm Collins – Plaintiff Forensic Investigator Malcolm Collins – Plaintiff Forensic Investigator Stored in Octoforensic’s Evidence Room
```
```
003
```
```
4/15/2023
0837 Malcolm Collins – Plaintiff Forensic Investigator Malcolm Collins – Plaintiff Forensic Investigator Stored in Octoforensic’s Evidence Room
003 4/17/2023
0800
```
```
Blaine Milburn - Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Retrieved for Forensic
Investigation
003 4/17/2023
1300
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Blaine Milburn - Plaintiff
Forensic Investigator
```
```
Stored in Octoforensic’s
Evidence Room
004 4/19/2023
1700
```
```
Blaine Milburn - Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Stored in Octoforensic’s
Evidence Room
001 4/20/2023
0730
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Removed from
Octoforensic’s Evidence
Room for Transfer
002 4/20/2023
0730
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Removed from
Octoforensic’s Evidence
Room for Transfer
003 4/20/2023
0730
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Removed from
Octoforensic’s Evidence
Room for Transfer
004 4/20/2023
0730
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Removed from
Octoforensic’s Evidence
Room for Transfer
001 4/20/2023
0900
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Patrick Messer #012 IPD Evidence Storage
002 4/20/2023
0900
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Patrick Messer #012 IPD Evidence Storage
003 4/20/2023
0900
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Patrick Messer #012 IPD Evidence Storage
004 4/20/2023
0900
```
```
Malcolm Collins – Plaintiff
Forensic Investigator
```
```
Patrick Messer #012 IPD Evidence Storage
```
IPD_Form_#PE003_v.1 (12/2012) Page 1 of 2 pages (See back)

## References.............................................................................................................................

BasisTech. (2023, April 21). _Autopsy_. Retrieved from Autopsy: https://www.autopsy.com/about/

EaseUS. (2023, February 22). _What Does Format Disk Mean?_ Retrieved from EaseUS:
https://www.easeus.com/computer-instruction/what-does-format-disk-mean.html

ElectroParts. (2023, March 28). _LG 65" 65SK8000PUA EBT65139702 Main Video Board Motherboard Unit_.
Retrieved from EletroParts: https://www.electropartsonline.com/lg-65-65sk8000pua-
ebt65139702-main-video-board-motherboard-unit.html


Exterro, Inc. (2023, April 21). _FTK® Forensic Toolkit_. Retrieved from Exterro:
https://www.exterro.com/forensic-toolkit

Gupta, P. (2013, February 25). _HP sells webOS operating system to LG Electronics_. Retrieved from
Reuters: https://www.reuters.com/article/hp-webos/hp-sells-webos-operating-system-to-lg-
electronics-idINDEE91O0G120130226

Infosec Institute, Inc. (2018, February 4). _File Carving_. Retrieved from Infosec Institute:
https://resources.infosecinstitute.com/topic/file-carving/

Kięczkowska, K. (2022, November 8). _USB Forensics 101_. Retrieved from InfoSec Write-ups:
https://infosecwriteups.com/usb-forensics-101-444faf737c4c

LG, Inc. (2023, March 28). _SK8000PUA 4K HDR Smart LED SUPER UHD TV w/ AI ThinQ® - 55'' Class (54.6''
Diag)_. Retrieved from LG: https://www.lg.com/us/tvs/lg-55SK8000PUA-4k-uhd-tv

Matheson, G. (2015). _Evidence Handling, Processing and Tracking._ Washington D.C.: National
Commission on Forensic Science.

Mehta, P. (2022, July 22). _Use Of The DoD 5220.22-M Standard For Drive Erasure_. Retrieved from
BitRaser: https://www.bitraser.com/article/DoD-5220-22-m-standard-for-drive-erasure.php

National Institute of Standards and Technology. (2023, April 2023). _Cryptographic hash function_.
Retrieved from National Institute of Standards and Technology:
https://csrc.nist.gov/glossary/term/cryptographic_hash_function

Rouse, M. (2016, December 21). _Address Resolution Protocol Cache_. Retrieved from Techopedia:
https://www.techopedia.com/definition/27470/address-resolution-protocol-cache-arp-cache

Stim, R. (2023, January). _Copyright Registration and Enforcement_. Retrieved from Standford Library:
https://fairuse.stanford.edu/overview/faqs/registration-and-enforcement/

United States Copyright Office. (2023, March). _A Brief History of Copyright in the United States_.
Retrieved from Copyright: https://www.copyright.gov/timeline/

Yasar, K. (n.d.). _MAC address (media access control address)_. Retrieved from TechTarget:
https://www.techtarget.com/searchnetworking/definition/MAC-address


