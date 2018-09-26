# 2018  OpenCV Meeting notes

[Template here](http://code.opencv.org/projects/opencv/wiki/Template)

[Markdown Syntax](https://guides.github.com/features/mastering-markdown/)

[[Meeting_notes]]

# Template

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-mm-dd

## __*Agenda*__
* 

### *__Minutes__*
* 

### *__To Dos__*
* Name
  - [ ] todo

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-09-26

## __*Agenda*__
* OSVF
* Documentaries

### *__Minutes__*
* OSVF
   * Setting up donations policy
      * We have an older attempt at the donation [give and get are here](https://docs.google.com/document/d/1bjvTVBejUGRuOLwkygKtvi9evBAOo2edXEAg7do0H7s/edit#heading=h.n2l2mkfzoywn)
   * First workshop/conferencette being considered
* Documentaries
   * Grace and I were filmed by a professional crew over 4 days for a large web production. Should come out in 2 months or so
   * Tonight I will give an OpenCV interview on the cable web show Future talk.

### *__To Dos__*
* Gary
  - [ ] Ideas feedback with Vadim
  - [ ] Put Sophia on GSoC deadline watch and organization
  - [x] Financials to IRS
  - [ ] Upload OSCON talk to Github
  - [ ] Expose OSCON tutorials on the coureware links
  - [ ] Courseware on OpenCV site

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-09-12

## __*Agenda*__
* OpenCV4
* Foundation
* HW

### *__Minutes__*
* OpenCV4
   * Beta Release next week, probably Wednesday
   * Final release by end of October
   * C++11 and tested against C++17
   * W image out
* Foundation
   * Federal status ongoing -- financials needed. This could take 1-3 months, all depends on IRS
   * Have talked with people to develop courseware camera modules
   * Conference venue in the works
   * Board meeting in next couple weeks

### *__To Dos__*
* Gary
  - [ ] Ideas feedback with Vadim
  - [ ] Put Sophia on GSoC deadline watch and organization
  - [x] Financials to IRS
  - [ ] Upload OSCON talk to Github
  - [ ] Expose OSCON tutorials on the coureware links
  - [ ] Courseware on OpenCV site

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-08-15

## __*Agenda*__
* Updates back from vacations

### *__Minutes__*
* Updates. OSVF can now do business as:
1. Open Source Vision Foundation
1. Open Source Computer Vision Library
1. OpenCV
1. Open3D
1. CARLA

### *__To Dos__*

* Gary
  - [x] Go through filming considerations
  - [-] Evaluate Moriah's OpenCV webiste changes

<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-07-25

**`Summer Vacation is upon us. Next report on August 15, 2018`**

## __*Agenda*__
* Foundation News

### *__Minutes__*
* Foundation News
   * OSVF logo is updated:
![OSVF](https://github.com/garybradski/wiki_images/blob/master/main_logo-300x263%402x.jpg)
   * Filing DBA announcements so that money wires or checks can go to any of the sub-orgs
       * Bank account will then be updated
   * Federal filing underway
   * [Umbrella website](http://www.osvf.org/)
   * Victor Eruhimov joins as the board member representing [OpenCV](https://opencv.org/)
 * August vacation hit. See y'all on Aug 15!

### *__To Dos__*
* Gary
  - [ ] Upload OSCON talk to Github
  - [ ] Expose OSCON tutorials on the coureware links
  - [ ] Evaluate Moriah's OpenCV webiste changes




<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-07-18

## __*Agenda*__
* [OSVF](http://www.osvf.org)
* OSCON
* OpenCV4

### *__Minutes__*
* [OSVF](http://www.osvf.org)
![OSVF logo](http://www.osvf.org/wp-content/uploads/2018/07/OSVF-Logo-256x300.png)
   * OSVF.org is a non-profit organization dedicated to advancing the beneficial uses of intelligent computer vision in society.
      * As in the above link, the website is live but still being constructed
      * See planning details [below](https://github.com/opencv/opencv/wiki/2018#minutes-2)
   * Secured a URL for future conferences/tutorials: Computer Vision Dev Con, CVDevCon.org
* [OSCON](https://conferences.oreilly.com/oscon/oscon-or)
   * We gave an extensive tutorial at the Open Software Foundation 
   * Material for [OpenCV Tutorial is here](https://github.com/xperience-ai/oreilly_opencv_workshop2018)
      * This covers the use of the [OpenCV Deep Neural Net Module](https://github.com/opencv/opencv/tree/master/modules/dnn) that is able to run inference on any trained deepnet model
         * A growing list of [curated deep neural network models for DNN is here](https://github.com/opencv/opencv/tree/master/samples/dnn)
         * [DNN Documentation is here](https://docs.opencv.org/3.3.0/d2/d58/tutorial_table_of_content_dnn.html)
       * See some of the opencv deepnet (DNN) tutorial for [pose](https://github.com/xperience-ai/oreilly_opencv_workshop2018/blob/master/python/DeepLearning/pose/OpenPose.ipynb) and [object detection](https://github.com/xperience-ai/oreilly_opencv_workshop2018/blob/master/python/DeepLearning/object_detection/tf_object_detection.ipynb)
* OpenCV 4
   * Release 3.4.2 is out, see [notes here](https://github.com/opencv/opencv/wiki/ChangeLog#version342) with further extended dnn module, documentation improvements, some other new functionality and bug fixes.

![](https://github.com/opencv/opencv/wiki/images/dnn.png)

-   DNN 3.4.2 improvements

    - Added a new computational target `DNN_TARGET_OPENCL_FP16` for half-precision floating point arithmetic of deep learning networks using OpenCL. Just use `net.setPreferableTarget(DNN_TARGET_OPENCL_FP16)`.
    - Extended support of Intel's Inference Engine backend to run models on GPU (OpenCL FP32/FP16) and VPU (Myriad 2, FP16) devices. See [an installation guide](Intel%27s-Deep-Learning-Inference-Engine-backend) for details.
    - Enabled import of [Intel's OpenVINO pre-trained networks](https://software.intel.com/openvino-toolkit/documentation/pretrained-models) from intermediate representation (IR).
    - Introduced custom layers support which let you define unimplemented layers or override existing ones. Learn more in [a corresponding tutorial](https://docs.opencv.org/3.4/dc/db1/tutorial_dnn_custom_layers.html).
    - Implemented a new deep learning [sample](https://github.com/opencv/opencv/blob/3.4/samples/dnn/text_detection.cpp) inspired by [EAST: An Efficient and Accurate Scene Text Detector](https://arxiv.org/abs/1704.03155v2).
    - Added a support of YOLOv3 and image classification models from [Darknet framework](https://pjreddie.com/darknet/).
    - Reduced top DNN's memory consumption and improvements in support of networks from TensorFlow and Keras.
   * 4.0 will come out in the Fall.

### *__To Dos__*
* Gary
  - [ ] Evaluate Moriah's OpenCV webiste changes
  - [x] Link to courseware
  - [x] Continue to advance OSVF.org site
* Victor
  - [x] Permission to take a board seat


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-07-11

## __*Agenda*__
* OSVF
* OpenCV4
* OSCON


### *__Minutes__*
* **OSVF**
   * OSVF is an umbrella foundation covering the following organizations
      * [**OpenCV.org**](http://opencv.org/) -- Free and Open Source Computer Vision code plus optimized deep learning
      * [**Open3D.org**](http://open3d.org/)  -- Free and Open 3D point cloud library code
      * [**CARLA.org**](http://carla.org/) -- Free and Open autonomous driving simulator
      * [**SVDLG**](http://www.svdlg.com/) -- Silicon Valley Deep Learning Group
      * Each of these orgs will retain their identity and will be run wholly by their own technical boards, but will cooperate to build a greater whole
       * Their responsibilities are to advance and maintain their respective platforms
   * OSVF is responsible for
      * Education:
         * Put on the Computer Vision Developer's Conference (CVdevcon)
            * CVdevcon will be distinctly different from other vision conferences
               * If will be largely tutorial, development and business focused
               * It will have an "unconference component" meant to facilitate business, solve outstanding vision issues, set standards/challenges adopt certifications etc
      * Run tutorial workshops
      * Develop courseware, hardware and software kits for learning intelligent computer vision
      * Infrastructure: 
         * Oversee and help the orgs maintain and advance free and open tools and infrastructure for intelligent computer vision
      * Standards and Certification: 
         * Drive standards and hardware/software certifications that help society absorb computer vision
      * Solve Problems: 
         * Set challenges and contests to solve significant problems in computer vision with beneficial impact for society
* **OpenCV4.0**
   * Coordinated delayed to Sept timeframe better align with other projects
   * Some of the changes are in or showing up in the 3.4 branch
   * It is still possible that there will be some earlier alpha releases so that it's "pre hardened"
* **OSCON (Open Source Convention)**
   * OpenCV is giving a tutorial there, [see the tutorial link](https://conferences.oreilly.com/oscon/oscon-or/public/schedule/detail/68133), Description:
   > _"Gary Bradski, Anna Petrovicheva, and Satya Mallick offer an overview of OpenCV and explain where it is going. Along the way, you’ll learn how to program some fun things that can be used for art, robotics, drones, film, and photography."_
   * Gary is going to also use it to announce the Open Source Vision Foundation

### *__To Dos__*
* Gary
  - [x] New logo
  - [x] New web designs
  - [ ] Link to courseware
  - [x] Get URL for future conference and workshops
  - [x] Access to OpenCV.org and webiste changes
  - [x] Complete signatures for the federal non-profit filings
* Victor
  - [ ] Permission to take a board seat

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-06-27

## __*Agenda*__
* OSVF
* OSCON


### *__Minutes__*
* OSVF
   * Bylaws and foundation documents are signed and with Adler and Colvin
   * Raising preliminary funds (about $20K committed) for formation expenses
   * Initial board: Gary, Vladlen, Achin, Vadim, Qian-Yi and German
      * Then each project, OpenCV, Open3D and CARLA will have their own technical boards to set development
   * Logo ideas:  Third eye (but camera?) but work in Kaniza triangle (but in 3D?) and neon color spreading
      * [Third eye theme](https://www.dreamstime.com/stock-illustration-third-eye-vector-mystical-sign-image61575538) ... oh, some symbolism that ultimately we are creating code for perception, not vision ... perception is what the mind makes of sensory stimuli. Also, CARLA is somewhat fabricating the mind's eye vision
      * [Illusory triangle](https://en.wikipedia.org/wiki/Illusory_contours#/media/File:Kanizsa_triangle.svg) Because perception is much more than vision -- we impose (causal) models on the world and the eventual smart machines must do so too.
      * [But lift the triangle to illusory 3D](http://illusionoftheyear.com/2011/05/impossible-illusory-triangle/) because, we are dealing with a 3D world ... and also Open3D!
* OSCON
   * We are going to give a course at OSCON
   * [Fun in detail with OpenCV](https://conferences.oreilly.com/oscon/oscon-or/public/schedule/detail/68133)

### *__To Dos__*
* Gary
  - [ ] New logo
  - [ ] New web designs
  - [ ] Link to courseware

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-06-13

## __*Agenda*__
* OpenCV 4.0
* DNN
* Foundation

### *__Minutes__*
* OpenCV 4.0
   * Joining components in other open sources, don't think I can mention
   * Target early August release ... 
      * integrating Halide subset
      * refactoring
* DNN
   * DNN can take advantage of optimize frameworks
* Foundation
   * Going to sign for California non-profit for Open Source Vision Foundation OSVF.org next week
      * Federal filing will take an additional month
      * 3 orgs in one, all can operate under their names: OpenCV.org, but all are also OSVF.org
         * The accounting will track separate donations to each org or to the general org
      * Educational focus
         * Conferences
         * Workshops
         * Contests
         * Courseware
         * Tutorials, internationally
         * Autonomous driving and robotics sensory intelligence
    * Standardized deep APIs, object proposal, segmentation encode/decode
* OSCON 
   * Tutorial is set: Me, Anna and Satya, have to get a room

**Next week is CVPR 2018 where some of us will be**

### *__To Dos__*
* Gary
  - [x] Sign the foundation legal docs after review
  - [ ] New logo
  - [ ] New web designs
  - [ ] Link to courseware
  - [x] Fund raise -- probably need more to pay legal fees and pay for OSCON prior to OSVF becoming final

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-06-06

## __*Agenda*__
* OSVF
* OSCON

### *__Minutes__*
* OSVF
   * Domain names secured
   * Legal meeting is all a go, 
       * Have to re-read final docs including the potential to do commercial/non-profit fellow travelers
       * Discussed how we can have for profits working with the non-profit. Each will be case by case with the legal firm
          * The non-profit can generate IP that can be licensed to a for profit
          * Doing certifications probably work, but have to be checked case by case
       * Have a (major) legal firm that will represent OSVF pro-bono
   * Have/will discuss on getting courseware going, Satya, Shiqyi etc
   * Met with Achin, he will help out as kind of a COO with Vladlen as kind of a CTO
      * Achin has a lot of experience putting on conferences/workshops and a lot of connections with people who know how to get this done.
      * Gary has ideas on what would differentiate this from other gatherings
   * Have Sofia, who wants to help out, also good at organizing events
   * We've been developing a bunch of leads for getting in real funding
   * Executive search
      * I have one lead on a CEO and am
      * Am considering, funding dependent, on engaging an executive search committee
   * OSVF will cover OpenCV, DNN (curated optimized deepnets) Open3D and ...
      * On Thursday, meeting with German and Vladlen about expanding OSVF further ... might be great synergy
 
* OSCON
   * We signed up for a tutorial at OSCON on July 17. 
      * Gary is head's down at Arraiy on product, and on foundation work
      * Vadim is focused on getting out OpenCV 4.0
      * Edgar is moving to London for some months to work with a group there
      * In summary, Gary can do an overview, but no time to prepare a tutorial, there others are out
         * Seeing if Satya can prepare the tutorial, if not, we may have to cancel, hope not

### *__To Dos__*
* Gary
  - [x] Contact Satya on tutorial
  - [x] Chase down CEO lead -- meet next month
  - [x] Finish reading the legal docs
  - [x] Thursday expansion meeting
  - [~] ~Return the signed forms to the lawyers for filing.~ _Deferred to next week_

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-05-23

## __*Agenda*__
* osvf
* OpenCV 4.0

### *__Minutes__*
* osvf
   * meeting with laywers tomorrow
   * [Staya ](https://www.learnopencv.com/about/) working on courseware
   * workshops conference
   * Stork involved?
   * Operating overseas?
      * free software foundation
         * free software foundation Europe
         * free software foundation Italy
      * Wikimedia
         * Separate in countries
      * Possible model is [intelliCAD](https://en.wikipedia.org/wiki/IntelliCAD)
    * Look into the [Transnational Giving Europe](http://www.transnationalgiving.eu/faq)
    * Coupling OpenCVlabs with osvf etc
* OpenCV4
   * DNN, ONNX support
   * QR reader, Halide
   * External interface will mostly remain the same
   * Works with [OpenVino framework](https://software.intel.com/en-us/openvino-toolkit)
      * opencv openVX DNN
      * IR Intermediate Representation
      * Face, pedestrian, license plate, age, gesture

### *__To Dos__*
* Gary
  - [x] Have the meeting with Adler & Colvin
      - [x] Ask about operating internationally
      - [x] Boundary of non-profit for profit and relationship (non-profit owning stock in for profit?)
  - [x] Update Shiqi Yu
  - [x] Discuss with VCs/finding CEO and bizdev partner roles

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-05-16

## __*Agenda*__
* Courses/partnerships
* osvf.org  *.labs

### *__Minutes__*
* Talked with Satya about org plans
   * Likes them
   * Interested in developing courseware share with OpenCV
   * Will meet either up in Silicon Valley or in San Diego to discuss further roles and possibilities
* osvf *.org *lab.com
   * Meeting with [lawyers](https://www.adlercolvin.com/our-firm) May 24 to get operating parameters of expanded org
   * Have team for Open3D
      * Vladlen to help out in advising/directing osvf in general
      * Qian-Yi and Jaesik to continue as Merge master and key contributor respectively for this
   * Have increasing numbers of initial and ongoing funding promises
   * Goal is to have an up and running expanded org before July.

### *__To Dos__*
* Gary
  - [x] Finish new legal docs


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-05-09

## __*Agenda*__
* Reorg
   * osvf
   * Open3D


### *__Minutes__*
* Reorg
   * Working on re-filing OpenCV.org to be done more legally correct
      * I've turned in all the forms (about 50-60 pages) to non-profit specialists [Adler & Colvin](https://www.adlercolvin.com/our-firm)
         * I will be talking with them May 26
      * New board, state and federal filings etc
      * Big name law firm will handle legal affairs pro-bono
   * Expanding the role of OpenCV into a more encompassing organization
      * Joining together with [Open3D](http://www.open3d.org/)
   * Exploring a new crowdfunding directions -- bid $s on where you want things to go
   * Have many ideas for what the org can do, but first, the usual things
* OpenCV 4.0 will be out this summer, might fold in the same methodology with Open3D later

### *__To Dos__*
* Gary
  - [ ] Talk to VCs about finding a business leader, possibly shared with OpenVlabs
  - [x] Talk with Satya


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-05-02

## __*Agenda*__
* Non-profit refile
* Future licensing
* OpenCVLabs

### *__Minutes__*
* Non-profit refile
   * I've given probably 40-50 pages of docs to the firm of  [Adler & Colvin](https://www.adlercolvin.com/our-firm) specializing in non-profits
      * Since they are familiar with the original material, it should only take a week or two
      * California re-formation and Federal formation
      * After filing, a very major law firm will represent us pro-bono
   * Courseware
      * Consider [ideas from Kubernetes](https://www.cncf.io/certification/expert/cka/)
   * Certification
      * Consider example from SwRI
         * [Oil lubricant certification](https://www.swri.org/industries/lubricant-testing)
         * [Gasoline engine oil engine testing](https://www.swri.org/passenger-car-lubricant-testing)
         * [Fuel certification](https://www.swri.org/fuel-analysis)
         * But in computer vision
            * Develop Standards
               * _OpenCV Inside_, _OpenCV Certified_
            * Camera and Algorithm
               * Quality & Performance
               * Accuracy of claims
               * AR, VR, SLAM, Recognition, Robotic Perception, Tracking, Detection ...
        * Certification of people
            * Take [example from Kubernetes Administrator](https://www.cncf.io/certification/expert/cka/)
            * Or for corporate [(taken from Kubernetes Providers](https://www.cncf.io/certification/kcsp/)
   * Funding
      * Corporate Grants
         * In China, in US
      * Government Grants
         * In China, in US, ... in Europe
      * Will obviously need to start working internationally
* Future licensing
   * Consider using the Linux Foundation ID together with github:
      * [Signing up as corporate or individual contributor ID](https://github.com/kubernetes/community/blob/master/CLA.md)
         * [Corporate conribution agreement license ID](https://github.com/cncf/cla/blob/master/corporate-cla.pdf)
         * [Individual contribution agreement license ID](https://github.com/cncf/cla/blob/master/individual-cla.pdf)
         * [Then when you or corp contribute, you turn on your ID](https://camo.githubusercontent.com/cdcaa8a1b2679acb1c8452091a05e27c8e68bc54/687474703a2f2f692e696d6775722e636f6d2f74456b3278336a2e706e67)

### *__To Dos__*
* Name
  - [x] Talk to Vladlen
  - [ ] Talk to VCs about finding a business leader, possibly for OpenCVLabs


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-04-18

## __*Agenda*__
* Porting
* OpenCV 4.0

### *__Minutes__*
* Transition tools
   * Clang-tidy helping to bump OpenCV API
* OpenCV 4
   * 3.4 is for remaining releases in 3.X
   * DNN updates open pull requests and bugs
   * OpenCV 4
   * 20 specs for [OpenCV github evolution](https://github.com/opencv/opencv/wiki/Evolution-Proposals)
       * C++11 or 14?
       * AV1 out a few weeks ago, most majors behind it. Support it.
* OpenCVLabs
    * Domain name secured, might use for supporting commercial activities


### *__To Dos__*
* Gary
  - [x] Finish off legal work on .org
     - [x] Contact legal firm about finishing this off
  - [x] Put OpenCV Evolution onto main page
  - [x] Talk with Shiqi Yu on education

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-04-11

## __*Agenda*__
* Release updates
* Legal update
* Future directions

### *__Minutes__*
* Release updates
* Legal update
* Future directions
   * Possible to get into smart camera + courseware
      * [Thousand Talents Program](https://en.wikipedia.org/wiki/Thousand_Talents_Program_(China))
      * [Foreign academician of Chinese Academy of Engineering](http://www.casad.cas.cn/chnl/315/index.html)


### *__To Dos__*
* Name
  - [ ] todo

# Notes:







<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-03-28

## __*Agenda*__
* OpenCV 4
* Foundation ideas, Vadim visit to China
* Linux foundation, deep learning

### *__Minutes__*
* Work started on OpenCV 4
   * C++ 11
   * Halide
   * More deep nets
* Shenzhen visit, Chinese branch of OpenCV
   * Education - courseware
      * Deep learning, vision
   * Work on OpenCV -- best students china summer of code
      * China summer of code
   * Robot arms
      * Education arm
      * Cheap real arm
   * Raspberry PI with smarts
* [Deep learning Linux foundation](https://www.linuxfoundation.org/projects/deep-learning/)
   * Consider if it's worth associating


### *__To Dos__*
* Name
  - [ ] Vadim send org ideas from trip
  - [ ] Gary finish up legal work

# Notes:

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-03-14

## __*Agenda*__
* Just touch base
* Contractors

### *__Minutes__*
* Google helping squash security issues ... these should all be upstream/incorporated by now
* Trying to help kickstart another group of contractors
* Future evolution of OpenCV [here: github evolution](https://github.com/opencv/opencv/wiki/Evolution-Proposals)
  * This will form the pool of properly formatted future GSoC ideas as well as a list to be vetted and implemented
* Vadim on week 1 of vacation

### *__To Dos__*
* Gary
  - [^] Finish reading all legal docs and contact lawyers


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-03-07

## __*Agenda*__
* Org filings
* Posting wishes for OpenCV it's evolution

### *__Minutes__*
* Org ideas
   * Competency centers (logo) 
       * Network of people who know, system integrator, supplier ...
       * Computer vision center in Barcelona for example
   * Set up a foundation meta group (such as drone vision code) area as done by the [Linux Foundation](https://www.linuxfoundation.org/projects/)
       * Could be medical, robotic, drone, AR, VR, Maps, Pictures and film ...
* Release
   * OpenCV 3.4.1 release is out
* OpenCV Evolution
   *  New ideas for what should be in OpenCV that could also feed, say, into [GSoC OpenCV Ideas](https://github.com/opencv/opencv/wiki/2018) will go onto [github evolution](https://github.com/opencv/opencv/wiki/Evolution-Proposals)
* 2 weeks vacation, national holliday ... Vadim



### *__To Dos__*
* Gary
  - [^] Finish reading all legal docs and contact lawyers
* Edgar
  - [ ] Vision Center in Barcellona contact as competence center
* All
  - [ ] Send in org ideas or comment on the formation docs I sent around

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-02-28

## __*Agenda*__
* Org docs
* OSCON
* OpenCV 4

### *__Minutes__*

* Org docs
   * Gary sent around to the nominal future board a document about amending and restating OpenCV.org
   * Once Gary gathers feedback, this will go to Adler & Colvin (legal firm that specializes in non-profit filings) to file federally
   * Key points:
      * Org will host the code, programmers and offer support packages/instant bug fix for the library
      * Org will advance the state of vision via developing algorithms and/or more useful APIs
      * Org will run gatherings: workshops, conferences, hackathons, educational events
      * Org may offer courseware
      * Org may offer smart camera HW/SW kits
         * For education
         * For contests (First Robotics)
         * For public demonstrations
         * For art
      *  Can host datasets for contests, reference, challenges/awards
         * Possibly labeling tools
      * Will be able to offer certification services for cameras, software or combinations
* OSCON
   * We've been asked to do a 3 hour tutorial at OSCON 2018. This is in preparation with Anna Petrovicheva of Xperience.ai
* OpenCV 4.0
   * Out this summer, much more seamless support for deep nets.
   * To set future direction of the library, we are going to 
      * use something like the [swift evolution list](https://github.com/apple/swift-evolution/tree/master/proposals)
     * suggested [opencv evolution format here](https://github.com/vpisarev/opencv/wiki/OpenCV-Evolution-Proposals)
     * adding in some from [GSoC ideas format](https://google.github.io/gsocguides/mentor/defining-a-project-ideas-list)
   * Consider adding some frameworks: Object detection: take frame by frame, rectangles w/confidence on output

### *__To Dos__*
* Gary
  - [ ] ~~Org setup~~ -- too vague, break it down above
* Vadim
  - [x] Ask Maxime (spelling?) how to add images to the OpenCV wiki/website. Now that it is GIT based, you have to link to an image somewhere, can be a specialized GIT repository for this.


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-02-21

## __*Agenda*__
* Go over federal non-profit org
* OSCON
* Brainstorm on new focuses
* OpenCV release and 4.0


### *__Minutes__*
* Org filing
* New release
   * 3.4.1 Release end of week
      * Support for quantized models in DNN
      * Face detection module is now 2.7M, works way better than Haar
      * Many patches and fixes
      * Likely last release of 3 series, work starts on 4.0 version
         * Support for 3.4 will not stop, it will be supported for some years
   * 4.0
      * Sometime mid-July.
      * Will have wiki linked to GIT feature "evolution" proposals 
         * That people or corporations can fund
         * And will form a more GIT linked feature list for future GSoC Ideas list
         * Submit feature request to GIT bug tracker request
            * Will be on wiki -- all a github repository
            * Ask Maxime where Wiki images should go
   * HighGUI  can we combine 2D and 3D, camera trajectories (uses VIS right now)
      * How to render fonts ... text rendering ... use gtk or other
      * Replace QT functionality, write real buttons
      * Several proposals to put this together 
      * Will put it on the new "evolution" issues page to come.
      
* OSCON
   * Beta or Alpha 4.0 release will be out
   * Tutorial -- intro future of opencv, new org, new feature request ways to join/help
      * DNN -- face tracker, other (how to squash a net??)
      * Python interface use
      * Some examples that support ... interactive art (face, body tracking) or robotics
* New focuses
   * Robotics
      * Support First Robotics with a basic recognition kit (2D, 3D ...)
      * Courseware kit?
   * Arts
      * Interaction


### *__To Dos__*
* Gary
  - [ ] Org setup
  - [x] Get paypal data to accountant
* Vadim
  - [ ] Ask Maxime (spelling?) how to add images to the OpenCV wiki/website. Now that it is GIT based, you have to link to an image somewhere, can be a specialized GIT repository for this.

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-02-14

## __*Agenda*__
* _**Happy Valentines Day!**_
* New meeting time, **9:30am Wednesday Californa time**
* GSoC
* Idea list
* Org structure

### *__Minutes__*
* **GSoC** 
   * Didn't get in this year ... we suppose the reasons (in order):
      1. Our ideas list was not [compliant](https://google.github.io/gsocguides/mentor/defining-a-project-ideas-list) ... no real excuses but: 
         * We are an older org, so only one grad student on our board, the rest are all working full-time professionals and/or running companies etc and we just picked up on the email warning about Google being serious about this item this year too late.
         * As with most of these items, one problem is that we've been in for many years and were just following patterns that had worked, but some things have changed, the emphasis on this is one, another rating point in the summer and so on.
         * _Corrective:_ is simply below -- make the list compliant 
      1. We were late in the 2017 mid-summer student rating, again, no excuse, but we were in the pattern from the previous year where this didn't exist and several of us just happened to be traveling.
         * _Corrective:_ (1) Is to make sure this doesn't happen, (2) I'm trying to get more money into the org so that we can hire some full time staff who can keep up with the greater demands on the org.
      1. We've been in for years -- they might have also decided we needed a kick/or to just rotate us out
         * _Corrective:_ Just apply again next year.
* **Idea List**
   * Have to get compliant with [Defining a Project Ideas list from the Mentor Guide](https://google.github.io/gsocguides/mentor/defining-a-project-ideas-list)
*  **Org Structure**
   * Traffic is up, OpenCV 4.0 is coming out this summer, we have major new content to digest from opencv_contrib and particularly incorporation of of the [deep neural network module DNN](https://docs.opencv.org/3.3.0/d2/d58/tutorial_table_of_content_dnn.html).
   * It's time to take the running of the org up a level:
      1. Refile the federal non-profit status, include hosting standards such as
         * Certifying camera/smart camera modules
         * Image datasets standards
         * Selling or partnering for education kits
      1. Recruiting or changing over to a more professional business and technical board
      1. Changing law firms to a bigger/scarier law firm that has offered to handle this pro-bono
      1. Recruiting a business manager and probably admin
      1. There is promised funding for some of this, need to convert promises to checks
      1. As a stretch goal, maybe run OpenCV Summer of Code at a small level this year:
         * DNN tutorial/ONNX to work well with ingesting major deep platform networks.
         * python
         * highGUI
* OSCON
   * Asked for a 3 hour tutorial ... Need to see if we can find someone to help or turn it down. Would like to say "yes"
* Open3D
   * Will be meeting with [vladlen koltun](http://vladlen.info/) about Open3D on Feb 15th

### *__To Dos__*
* Gary
  - [~] Org setup _started..._
* Vadim
  - [x] See if we have people to run the OSCON tutorial

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-02-06

## __*Agenda*__
* GSoC
* Halide
* Open3D

### *__Minutes__*
* GSoC
   * HighGUI person
   * tiny-dnn policy
* Halide plans/schedule
* Open3D
   * Will be meeting with [vladlen koltun](http://vladlen.info/) about Open3D on Feb 15th

### *__To Dos__*
* Gary
  - [ ] Org setup 
  - [-] Ask Yann about students for ONNX task
* Vadim
  - [-] Send name of contact person 

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-01-29

## __*Agenda*__
* Change meeting times 
* DNN

### *__Minutes__*
* New meeting time, 9:30am Wednesday Californa time
* DNN 
   * Backend (fusion, convolution)
      * C++
      * SSE, Neon ...
      * API is general
      * OpenCL
      * Halide (could generate CUDA, OpenCL or anything)
         * AMD graphics
* DNN work
* Halide ongoing
### *__To Dos__*
* Gary
  - [ ] Org setup 
  - [ ] Ask Yann about students for ONNX task
* Vadim
  - [ ] Send name of contact person 

<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-01-21

## __*Agenda*__
* GSoC Projects, mentors

### *__Minutes__*

* Now applied to GSoC
![OpenCV GSoC2018](https://github.com/garybradski/opencv/blob/master/samples/cpp/tutorial_code/images/done.png)
* GSoC Projects, mentors
   * tiny-dnn and DNN
      * How to resolve DNN and tiny-dnn
      * DNN runs inference 
      * ONNX
      * Integration with [TVM](http://tvmlang.org/) ... relationship to Halide
         * [Good timings](http://www.tvmlang.org/2018/01/16/opt-mali-gpu.html) 
* Opencv 4.0 
   * DNN integrated into core as a central function
   * Somethings move to conrib
* Geometric vision differences with deep learning
   * Deep learning 
* DNN runs inference 
   * Will stay in OpenCV
   * Will not have any dependencies
   * Can add extensions ... needs NVidia
   * 4 backends: 
      * C++ +intrinsics optimizations; 
      * OpenCL; 
      * Halide; 
      * DL Inference engine
      * Can we just open to different backends to allow extensions to NVidia, ARM?
         * [TVM](http://tvmlang.org/)?
            * But whole LLVM is in it
* deep ideas:
   * it would be nice to have self-contained ONNX importer (using libprotobuf?).
   * some network compression algorithms, probably including quantization and factorization-based methods (where compression algorithm itself can be implemented as pytorch or Caffe2 or TF script, but then OpenCV probably needs to be extended to parse such compressed networks).
   * we would also be interested in adding new layers that would help to support new interesting topologies. In particular, it would be cool to have supported some compact networks for text detection and for background segmentation, maybe shadow elimination, tracking etc. or whatever Yann considers to be worthy. 


### *__To Dos__*
* Gary
  - [ ] Org setup 
  - [x] Pay
  - [ ] Ask Yann about students for ONNX task
* Vadim
  - [x] Send Edgar OpenCV slides for U. Barcelona presentation



<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2018-01-15

## __*Agenda*__
* GSoC

### *__Minutes__*
* GSoC
   * OpenCV has officially applied to be an Org for 2018!
      * The [idea page is here](https://github.com/opencv/opencv/wiki/GSoC_2018)
   * Optimizing nets ... can be hard
      * Mobile net, u net for segmentation, for example VGG replaced by Mobile
      * Replace layer by layer with quantization, pruning
         * Fine tuning ... need to train
      * Hardnet descriptors
      * Features
   * Add support for ONNX ... 
      * Translating ONNX structures to be run in DNN
      * TensorFlow uses different memory layout than caffe
          * Smaller semantic differences
      * We have a good mentor for this, if we can find the student
      * MXnet ?
          * Generic compilation inside of graph
          * Halide part to generate ops and scheduling 
          * Python interface Keras API, CNTK
* Possible source of imagery from ...
   * Judge appropriateness or not of images
   * Judge affect of images on users
   * General applicability
* Fever seems over from flu...
      

### *__To Dos__*
* Gary
  - [ ] Org setup 
  - [ ] Pay
  - [ ] Ask Yann about students for ONNX task
* Vadim
  - [x] Send Edgar OpenCV slides for U. Barcelona presentation

# Notes


<pre>
<><><><><><><><><><><><><><><><><><><><><><><><><><><><><><><>
</pre>

## 2017-01-08

## __*Agenda*__
*  GSoC 2018
* Org ideas

### *__Minutes__*
* GSoC
  * Categories
     * Python
     * highGUI improvements
     * C to C++ translator
     * SLAM
     * Deep model curation/optimization
       * Better TensorFlow, Pytorch integration
* Org
  * Fully funded non-profit
  * Business basis
    * Image analysis
    * Seminars, workshops
    * Education, documentation

* Gary has the flu despite the vaccine ... and a headache.


### *__To Dos__*
* Gary
  - [x] Set up ideas page
  - [x] Set up 2018 Notes
  - [x] Apply for GSoC 2018
  - [ ] Org setup 
  - [ ] Pay





***



[[Meeting_notes]]