---
title: wiki-license-open-source-code
tags: [law, license, open-source]
created: 2020-07-13T03:29:04.214Z
modified: 2021-09-14T18:58:58.275Z
---

# wiki-license-open-source-code

# guide

- 修改后可闭源
  - Apache，BSD，MIT
- 修改后必须同样许可
  - GPL
- 修改后不能闭源
  - GPL/LGPL
  - MPL

- resources
  - https://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html
  - https://tldrlegal.com/
  - https://choosealicense.com/licenses/
  - linkware, watermark
  - [SPDX License List | Software Package Data Exchange (SPDX)](https://spdx.org/licenses/)
  - [Open Source License Usage_202008](https://solutionshub.epam.com/blog/post/examining-open-source-license-usage)
    - custom/32.7%, apache/27.8%, mit/26.3%, gpl/4.8%, agpl/1.40%, mpl/1.37%, others/3.4%
  - [Open Source License Compliance](https://fossa.com/blog/tag/open-source-license-compliance/)
  - [OSI Approved Licenses](https://opensource.org/licenses/)

- Copyright”指软件的版权和其它一切权利归软件作者所私有，用户只有使用权，没有其它如复制、重新修改发布等权利。
- 而“Copyleft”的特点是仅有版权归原作者所有，其他一切权利可以与任何人共享。
  - “Copyleft”通常被译作“著佐权”，即通过许可证的形式，补足、辅佐著作权（Copyright）不足的版权授权，相当于一种权利与义务的契约
# non-commercial

## BSL/Business Source License

- ref
  - [Business Source License 1.1 | MariaDB](https://mariadb.com/bsl11/)

- who is using #BSL-lic
  - couchbase
  - surrealdb
  - CockroachDB
  - outline-wiki
  - directus-cms
  - Sentry
  - HashiCorp consul: data center aware solution to connect and configure applications across dynamic, distributed infrastructure
  - kurtosis: Kurtosis shines when creating, working with, and destroying self-contained distributed application environments.

- [What Software License is Better - BSL, Source Available or Open Core?](https://devm.io/open-source/software-licenses-bsl-open-core)
  - The Business Source License was introduced by Michael Widenious (Monty) in 2013 and was initially used by MariaDB Corporation for some of the company’s software and not MariaDB Server itself.

## [Polyform Licenses](https://polyformproject.org/licenses/)

- SPDX支持
  - PolyForm-Noncommercial-1.0.0
  - PolyForm-Small-Business-1.0.0

- PolyForm Project publishes a suite of standardized licenses:
  - PolyForm Noncommercial is a general noncommercial license for software.
  - PolyForm Perimeter permits uses other than those that compete with the software.
  - PolyForm Shield permits uses other than those that compete with the provider of the software.
  - PolyForm Strict removes permission to distribute copies and make changes, leaving only permission to use for noncommercial purposes.
  - PolyForm Internal Use permits use for internal business purposes.
  - PolyForm Small Business permits use by small businesses and other small organizations.
  - PolyForm Free Trial permits a free, time-limited trial.

- https://news.ycombinator.com/item?id=24583479
  - If anyone is interested in using a source-available license for their own code, the Polyform Project has a set of standardized, source-available licenses. 
  - PolyForm Shield would probably achieve the same result as the Timescale License

## [Fair-code](https://faircode.io/)

- Fair-code is not a software license. 
- It describes a software model where software:
  - is generally free to use and can be distributed by anybody
  - has its source code openly available
  - can be extended by anybody in public and private communities
  - is commercially restricted by its authors

- The following existing licenses meet all the fair-code requirements and projects using any of them can use the "fair-code" term.
  - Commons Clause with any OSI approved open-source license
  - Elastic License 2.0 (ELv2)
  - Confluent Community License
  - Sustainable Use License

## non-commercial-faq

- [Open-source license to prevent commercial use](https://opensource.stackexchange.com/questions/4875)
  - There is now a license specifically designed to create source-available software for non-commercial use, namely the Commons Clause License.
  - Redis Labs 正在放弃其 Commons Clause 许可，转而使用新的“available-source”许可证

- [Can I license my project with an open-source license but disallow commercial use?](https://opensource.stackexchange.com/questions/9805)
  - There are several licences that disallow commercial use of the software (or other intellectual property). 
  - Most notably CC BY-NC 3.0 
  - If you want to reduce commercial use one of the more effective ways is to choose very strict licence like AGPL 3.0 and dual licence it with a commercial licence.
  - you can prevent your Open Source project from getting included in a closed-source project (for example, by using a GPL license), and then offer a dual-license option for companies who don't want to release their own proprietary code as open source.
# Apache Licence 2.0(ASLv2)
- ref
  - https://choosealicense.com/licenses/apache-2.0/
  - https://tldrlegal.com/license/apache-license-2.0-(apache-2.0)

- You can do what you like with the software, as long as you include the required notices. 
  - This permissive license contains a patent license from the contributors of the code.
- must include copyright/license/notice, state changes

- 特点
  - 非版权
  - 项目作品适合商业用途
  - 被许可方可以修改项目
  - 被许可方**必须提供引用说明**
  - 被许可方可以根据不同条款重新分配衍生作品
  - 被许可方不必将其衍生作品和源代码一起分发

- 类似于MIT，但它同时还包含了贡献者向用户提供专利授权相关的条款
  - 要求 协议和版权信息、声明变更
  - 允许 商用、分发、修改、专利授权、私用、附加协议
  - 禁止 作者免责、商标使用
- 允许代码修改、再发布
- 需要给代码的用户一份Apache License
- 如果你修改了代码，需要再被修改的文件中说明。
- 在延伸的代码中（修改和有源代码衍生的代码中）需要带有原来代码中的协议，商标，专利声明和其他原来作者规定需要包含的说明。
- 如果再发布的产品中包含一个Notice文件，则在Notice文件中需要带有Apache Licence。你可以在Notice中增加自己的许可，但不可以表现为对Apache Licence构成更改。
# Artistic
- ref
  - [Artistic License 2.0 – Open Source Initiative](https://opensource.org/license/artistic-2-0/)
  - [Open Source Licenses Demystified | Toptal®](https://www.toptal.com/open-source/developers-guide-to-open-source-licenses)

- The Artistic License, in its current version 2.0, is a permissive open-source license with no copyleft similar to the MIT license.
- The main difference between the MIT license and the Artistic License is that the latter requires that any modification made to the code must be clearly stated.
- This license is almost exclusively used in the Perl community.
- The current Artistic License 2.0 is compatible with GPL: you can mix Artistic-Licensed code into GPL software.
# MulanPSL - 2.0
- ref
  - https://opensource.org/licenses/MulanPSL-2.0

- Apache License要求列出每个修改文件，其实很多项目做不到这一点，所以MulanPSL直接取消了这项要求
# GPL (General Public License)
- ref
  - https://tldrlegal.com/license/gnu-general-public-license-v3-(gpl-3)

- GPLv3
  - You may copy, distribute and modify the software as long as you track changes/dates in source files. 
  - Any modifications to or software including (via compiler) GPL-licensed code must also be made available under the GPL along with build & install instructions.
  - must include copyright/license/original/build instructions, state changes, disclose source

- 特点
  - 版权约束很强
  - 项目工作适合商业用途
  - 被许可方可以修改项目
  - 被许可方必须将源代码与衍生作品一起发布
  - **衍生作品必须以相同的条款发布**

- you have to release source code if you link against and distribute the binary, but don't if you just provide a service
- 应用广泛
  - 要求 公开源码、协议和版权信息、声明变更
  - 允许 商用、分发、修改、专利授权、私用
  - 禁止 责任承担、附加协议
- GPL的出发点是代码开源 > 免费使用和引用 > 修改/衍生代码的开源 > 免费使用，但不允许修改后和衍生的代码做为闭源的商业软件发布和销售
- GPL规定：只要这种修改文本在整体上或者其某个部分来源于遵循GPL的程序，该修改文本的 整体就必须按照GPL流通，不仅该修改文本的源码必须向社会公开，而且对于这种修改文本的流通不准许附加修改者自己作出的限制。因此，一项遵循GPL流通的程序不能同非自由的软件合并。
- 任何一套软件，只要其中使用了受GPL协议保护的第三方软件的源程序，并向非开发人员发布时，软件本身也就自动成为受GPL保护并且约束的实体。也就是说，此时它必须开放源代码。
- 你可以去掉所有原作的版权信息，只要你保持开源，并且随源代码、二进制版附上GPL的许可证就行
- 无论软件以何种形式发布，都必须同时附上源代码。例如在Web上提供下载，就必须在二进制版本下载的同一个页面提供源码下载，如果以光盘形式发布，就必须同时附上源码
- 开发或维护遵循GPL协议开发的软件的公司或个人，可以对使用者收取一定的服务费用
- GPL只是规定用户在获取你的程序的时候必须可以获得源代码，但并没有规定必须免费
- 如果你的确需要发布你的程序，但又不想开源，规避GPL的方法是通过LPC或者RPC间接调用库里的接口。只要库和你的程序不运行在同一进程下，就不需要开源
# LGPL (Lesser GPL)
- ref
  - 修改后的源码和产物都必须同样以LGPL发布，对使用友好，对修改和发布不友好
  - https://tldrlegal.com/license/gnu-lesser-general-public-license-v3-(lgpl-3)

- who is using #lgpl-license

- This license is mainly applied to libraries. 
  - You may copy, distribute and modify the software provided that modifications are described and licensed for free under LGPL. 
  - Derivatives works (including modifications or anything statically linked to the library) can only be redistributed under LGPL, 
  - but applications that use the library don't have to be.
- must include copyright/license/original/build instructions, state changes, disclose source

- 特点
  - 版权约束较弱（受限于动态关联的程序库）
  - 项目作品适合商业用途
  - 被许可方可以修改项目
  - 被许可方**必须将源代码与衍生工作一起开源发布**
  - 如果你修改了项目，则必须以相同的条款发布修改后的作品
  - 如果你使用项目作品，无需以相同的条款发布衍生作品

- you can link against and don't have to release source code as long as you don't modify the library itself
- 主要用于一些代码库
  - 要求 公开源码、库引用、协议和版权信息
  - 允许 商用、分发、修改、专利授权、私用、附加协议
  - 禁止 责任承担
- LGPL是GPL的一个为主要为类库使用设计的开源协议
- LGPL允许商业软件通过类库引用(link)方式使用LGPL类库而不需要开源商业软件的代码。这使得采用LGPL协议的开源代码可以被商业软件作为类库引用并发布和销售。
- 如果修改LGPL协议的代码或者衍生，则所有修改的代码，涉及修改部分的额外代码和衍生的代码都必须采用LGPL协议。因此LGPL协议的开源代码很适合作为第三方类库被商业软件引用，但不适合希望以LGPL协议代码为基础，通过修改和衍生的方式做二次开发的商业软件采用。
- 采用LGPL的代码，一般情况下它本身就是一个第三方库，这时候开发人员仅仅用到了它的功能，而没有对库本身进行任何修改，那么开发人员也不必公布自己的商业源代码。但是如果你修改了这个库的代码，那么你修改的代码必须全部开源，并且协议也是LGPL，但除了库源码之外的商业代码，仍不必公布

- ## [The LGPL License - FOSSA](https://fossa.com/blog/open-source-software-licenses-101-lgpl-license/)
- As a copyleft license, LGPL requires users to release the source code of any changes to the original software
  - However, this requirement applies to a narrower set of code than the “regular” GPL.
  - A strong copyleft license (GPL v3, for instance) applies to the entire software program, including linked libraries and other components.
  - If you were to modify that LGPL-library and distribute it, then you’d have to release the changes. 
  - But **if your program simply uses the LGPL-library, there’s no need to share your source code for your part of the program**. 
  - You could even make your part of the program proprietary if you wanted to.
- The LGPL has different requirements depending on how the library is integrated with the remainder of the program. 
  - Generally, dynamic linking of LGPL code is considered best practice, as static linking makes meeting the license requirements more complicated. 
  - While it is possible to comply with LGPL code that is integrated into proprietary code as a statically linked library, it requires more effort. 
  - There is a kind of safe harbor for using LGPL code as a dynamically linked library; 
  - **for statically linked libraries, a distributor must offer access to not only the library’s source code, but other information or materials necessary to rebuild the program**. 
  - However, many programming languages have no equivalent of static linking, so that makes the dynamic linking safe harbor extremely helpful and effective in LGPL compliance.
- Like GPL, LGPL imposes no conditions on using the code in software that’s sold commercially.

- **LGPL is slightly different from other weak copyleft licenses, like the Mozilla Public License or Eclipse Public License, due to its special safe harbor for dynamic linking integration**.

- The LGPL does not permit sublicensing of the code, nor does it allow contributors to be held liable for legal issues or damages.
  - Like the MPL and CDDL, the EPL allows for sublicensing. 

- ## [Does compiling a JS bundle with webpack/browserify violate the LGPL license?](https://opensource.stackexchange.com/questions/5139/does-compiling-a-js-bundle-with-webpack-browserify-violate-the-lgpl-license)
  - In the case of Javascript, source code has to be understood as the source on which the programmer will make modifications, i.e. the non-minified source.
  - The compilation process is not going to produce a binary but a minified version of the code that should be considered "object code".
  - Thus, you can respect the terms of the license by releasing "object code" (the minified version) of the work using the library without the library itself. You could just put a link somewhere in your application so that users can download it.

- ## [Want to use LGPL licensed library, do I need to change license or configure linker in some way?](https://www.reddit.com/r/rust/comments/fevz37/want_to_use_lgpl_licensed_library_do_i_need_to/)
  - The LGPL does not forbid static linking, this is a common misconception. 
  - The LGPL doesn't need your project to be licensed under LGPL, nor does it require dynamic linking. 
  - All it requires you to do is to give abilities to modify the LGPL bits if they wish to (also, if you modify the LGPL bits you need to make your changes available under the LGPL) - that doesn't mean just giving people access to the LGPL source code, it means giving people the ability to run your application with arbitrary modified versions of the LGPL code. 
  - The easiest way to satisfy that requirement is via dynamic linking, but it's not the only one. 
  - If you give people access to the source code and the right to modify it (which you're normally doing with MIT licensed projects) that is one way to satisfy that requirement
  - If your project wasn't open source you still wouldn't technically be forbidden from static linking, but you'd still have to make it possible to swap out the LGPL bits (for example, by providing object files of your project), although this is getting into territories where it is a bit tricky to comply so some commercial projects just straight up ban the use of LGPL licensed code.
  - 👉🏻 The intent of the license is that a user should be able to substitute the library for their version
    - There are some possible approaches.
    - You can dynamically link the library. 
    - You can provide a separate dynamically linked library that wraps over an LGPL licensed crate with C compatible API and load it with a library like libloading.
    - You can provide the source code of your program. It doesn't have to be free software. 

- [LGPL protected file](https://github.com/jsdom/jsdom/issues/2642)
  - LGPL is suitable for a "dynamically-linked" file, but NOT for a "statically-linked" file. What do those terms mean in a JS context?
  - Using webpack, minify, etc to aggregate a JS/TS project (as is standard practice), makes the project into a "statically-linked" monolith - which makes the entire work into an GPL-derivative work. 

- [LGPL license in a concatenated JS file - Open Source Stack Exchange](https://opensource.stackexchange.com/questions/8063/lgpl-license-in-a-concatenated-js-file)
  - LGPL goes only for the code it's licensed under and for modifications of said code.
  - If the LGPL code would be in a separate file, then you would only open source that file under LGPL.

- ## [LGPL is more business friendly than GPL; it's literally "lesser" GPL.](https://news.ycombinator.com/item?id=35461088)
  - You can use LGPL in commercial, closed-source projects as long as you keep the LGPL code in a separate dynamically linked library, e.g. a DLL, and provide a way for users to swap it out for their own patched DLL if they wish. (Plus some other license terms.)
  - Also, you can always use LGPL code under the terms of the GPL, so there's no way LGPL is more restrictive than GPL.
  - Beware that you may need to be careful using LGPL code in a browser: JavaScript is source code not object code, arguing WASM is a DLL wouldn’t help, **most JavaScript minifiers perform static linking**, and sending LGPL code to the browser could be considered distribution. I always avoided all LGPL licensed libraries when doing commercial front-end work.
# MPL (Mozilla Public License)
- ref
  - 修改后的源码必须同样以LGPL发布
  - 产物可以不同license发布，**对修改友好**
  - 可以兼容GPL
  - https://tldrlegal.com/license/mozilla-public-license-2.0-(mpl-2)
  - [MPL 2.0 FAQ — Mozilla](https://www.mozilla.org/en-US/MPL/2.0/FAQ/)

- who is using #MPL-license
  - mozilla firefox/thunderbird
  - libreoffice

- MPL is a copyleft license that is easy to comply with. 
  - You must make the source code for any of your changes available under MPL, 
  - but you can combine the MPL software with proprietary code, as long as you keep the MPL code in separate files. 
  - Version 2.0 is, by default, compatible with LGPL and GPL version 2 or greater. 
  - You can distribute binaries under a proprietary license, as long as you make the source available under MPL.
- must include copyright/license/original, disclose source

- 特点
  - 版权约束较弱（受限于单个文件）
  - 项目作品适合商业用途
  - 被许可方可以修改项目
  - 被许可方必须提供引用说明
  - 被许可方可以根据不同条款重新发布衍生作品
  - 被许可方不得重新许可MPL许可的资源
  - 被许可方**必须将其衍生作品与MPL许可的源代码一起分发**

- MPL虽然要求对于经MPL许可证发布的源代码的修改也要以MPL许可证的方式再许可出来，以保证其他人可以在MPL的条款下共享源代码。
  - 但是，在MPL许可证中对“发布”的定义是“以源代码方式发布的文件”，这就意味着MPL允许一个企业在自己已有的源代码库上加一个接口，除了接口程序的源代码以MPL许可证的形式对外许可外，源代码库中的源代码就可以不用MPL许可证的方式强制对外许可。
  - 这些，就为借鉴别人的源代码用做自己商业软件开发的行为留了一个方式
- MPL许可证第三条第7款中允许被许可人将经过MPL许可证获得的源代码同自己其他类型的代码混合得到自己的软件程序。
- 要求源代码的提供者不能提供已经受专利保护的源代码
- 要求所有再发布者都得有一个专门的文件就对源代码程序修改的时间和修改的方式有描述
- MPL 2.0与Apache许可证以及GPL第二版或更新、LGPL2.1版或更新，及AGPL第三版或更新兼容。而1.1版因为有“一些复杂的限制”造成与GPL的不兼容（从而阻止升级到MPL 2.0）

- The MPL is a simple copyleft license. 
  - The MPL's "file-level" copyleft is designed to encourage contributors to share modifications they make to your code, while still allowing them to combine your code with code under other licenses (open or proprietary) with minimal restrictions.

- ## [Mozilla Public License 2.0 - FOSSA](https://fossa.com/blog/open-source-software-licenses-101-mozilla-public-license-2-0/)
- Weak copyleft licenses like the Mozilla Public License 2.0 also require users to disclose their changes to the source code, but requires sharing of a narrower set of code. 
  - If an author reworks any of the original files, they have to release those updates when distributing the code and license them under the MPL.
  - 👉🏻 However, **if the author keeps the MPL’d code in separate files, they can combine that code with closed-source code to create an aggregate work**. 
  - The new code files can be kept proprietary or released **under a different license**.
  - This is sometimes referred to as file-based copyleft.
- MPL 2.0 obligates users to state that the code is under the MPL license and share where they can find the license
- Sublicense binaries. **A developer may place binaries under a different license in the context of an aggregate work**.

- ### mpl vs lgpl
- Unlike the MPL, the LGPL does not allow users to sublicense the code. 
  - It also requires anyone who includes the code as part of a consumer device to include any installation information necessary to update and reinstall the software.

- ### mpl vs epl

- [What are some differences between MPLv2 and EPLv2?](https://opensource.stackexchange.com/questions/10860/what-are-some-differences-between-mplv2-and-eplv2)
  - The MPL is compatible with the GPL by default.
  - The EPL is not compatible with the GPL by default. 

- Both the MPL v2.0 and EPL v2.0 allow contributors to optionally release code either under the license by which it was originally released or under future published versions of the respective licenses. As far as I can tell, neither license implicitly upgrades to a future version

- These two licenses have a fair amount in common, including that both allow for aggregate works to be sublicensed. 
- One key difference is that the EPL offers additional legal protections to contributors.
  - Namely, any company that uses EPL’d code in commercial software must defend the code’s contributors should any lawsuits or damages arise regarding that software. Both licenses contain an explicit grant of patent rights.

- ## [How does the scope of the MPL's copyleft compare with the LGPL and GPL's copyleft?](https://www.mozilla.org/en-US/MPL/2.0/FAQ/)
- MPL: The copyleft applies to any files containing MPLed code.
- LGPL: The copyleft applies to any library based on LGPLed code.
- GPL: The copyleft applies to all software based on GPLed code.

- ## I want to use software which is available under the MPL. What do I have to do?
- Nothing. 
- Like all other free and open source software, software available under the MPL is available for anyone (including individuals and companies) to use for any purpose. 
- The **MPL only creates obligations for you if you want to distribute the software outside** your organization.

- ## I want to distribute (outside my organization) executable programs or libraries that I have compiled from someone else's unchanged MPL-licensed source code, either standalone or part of a larger work. 
- You must inform the recipients where they can get the source for the MPLed code in the executable program or library you are distributing (i.e., you must comply with Section 3.2). 
- You may distribute any executables you create under a license of your choosing, as long as that license does not interfere with the recipients' rights to the source under the terms of the MPL.

- ## I want to distribute (outside my organization) MPL-licensed source code that I have modified. 
- You must inform the recipients that the **source code is made available to them under the terms of the MPL** (Section 3.1), including any Modifications (as defined in Section 1.10) that you have created.
- You must respect the restrictions on removing or altering notices in the source code

- ## I want to distribute (outside my organization) an executable program based on MPL-licensed source code that I have modified. What do I have to do?
- You must **make available the MPL-licensed portions of the source code** as described in the previous question, and inform the recipients how they can obtain such source code

- ## If I use MPL-licensed code in my proprietary application, will I have to give all the source code away?
- No. The license requires that Modifications (as defined in Section 1.10 of the license) must be licensed under the MPL and made available to anyone to whom you distribute the Source Code. 
- However, new files containing no MPL-licensed code are not Modifications, and therefore do not need to be distributed under the terms of the MPL, even if you create a Larger Work (as defined in Section 1.7) by using, compiling, or distributing the non-MPL files together with MPL-licensed files. 
- This allows, for example, programs using MPL-licensed code to be statically linked to and distributed as part of a larger proprietary piece of software, which would not generally be possible under the terms of stronger copyleft licenses.
# EPL (Eclipse Public License)
- ref
  - 对修改友好，但默认与GPL不兼容
  - https://tldrlegal.com/license/eclipse-public-license-1.0-(epl-1.0)
  - https://www.eclipse.org/legal/epl-2.0/faq.php

- who is using #epl-license
  - eclipse jetty/golo
  - clojure

- This license, made and used by the Eclipse Foundation, is **similar to GPL** but allows you to link code under the license to proprietary applications. 
  - You may also license binaries under a proprietary license, as long as the source code is available under EPL.
- must include copyright/license/original, disclose source, compensate for damages

- EPL1.0 特点
  - 较弱的版权约束（受限于软件“模块”）
  - 项目作品适合商业用途
  - 被许可方可以修改项目
  - 如果你修改了作品，则**必须以相同的条款发布修改后的作品**
  - 如果你使用了作品，无需以相同的条款发布衍生作品
  - 软件的商业分销商必须在因商业用途导致的诉讼/损害中保护或赔偿原始EPL贡献者

- 对商用友好
  - 要求 公开源码、协议和版权信息
  - 允许 商用、分发、修改、专利授权、私用、附加协议
  - 禁止 责任承担

- ## [The Eclipse Public License - FOSSA](https://fossa.com/blog/open-source-software-licenses-101-eclipse-public-license/)
- As a weak copyleft license, the EPL is a middle ground of sorts between permissive options (like the MIT License or Apache License 2.0) and strong copyleft licenses (like GPL v2 and GPL v3.)
- A core requirement of the EPL — one that’s not part of permissive licenses — is that derivative works of EPL-licensed code must also be licensed under the EPL. 
  - (As such, anyone who distributes a program that constitutes such a derivative work must also make their source code available.)
- 👉🏻 However, the EPL’s definition for a derivative work is narrower than GPL’s.
  - **Under the EPL, if you simply use — rather than modify — an EPL-licensed component and keep it in a separate file, that would not constitute a derivative work, and you would not be required to make available your source code**. 
  - With the GPLs, however, any use (modified or not) of the licensed code would create a derivative work.
- Users can rework the code, but if they distribute these modifications, they must release these updates in source code form.
- Users can add a Secondary License to enable compatibility with GPL v2 or later

- ### EPL vs MPLv2
- A notable difference between the two is that the the MPL 2.0 does not include the EPL’s legal protections for project contributors.

- Like the EPL, the Mozilla Public License 2.0 allows users to keep (unmodified) MPL’d code in a separate file, then combine that code with code under a different license to create an aggregate work. The new/additional files can be released under a different license.

- ### epl vs lgpl
- A notable difference between the LGPL and other weak copyleft licenses is that the LGPL does not allow users to sublicense binaries under other terms, while the EPL and MPL 2.0 do.

- ## What are the major changes between EPL-1.0 and EPL-2.0?
- The term of art is now referred to as "file" rather than "module"; 
- The choice of law provisions has been removed; 
- The license is **now suitable for scripting languages such as JavaScript**; and
- The license now includes an option to add a secondary license for GPL-2.0+ compatibility.

- ## [EPL-Licensed Library with Closed-Source Commercial Product](https://softwareengineering.stackexchange.com/questions/152983/epl-licensed-library-with-closed-source-commercial-product)
- EPLv1 is copyleft, because it requires you to release any changes you made to the EPL code while working on your main app. 
- **The difference from GPL is that it's a commercial-friendly copyleft, requiring you only to make those changes available and only if you distribute your commercial app**. 
  - **And if you made no changes, no source code to release**

- You need to mention it includes EPL code, and allow them to request access to the source code of the EPL code if they want, including any modifications you've made to it. Your own code though, which only uses the EPL code in an import for example, does not need to be made EPL, and you do not have to give its source away

- ## Is my EPL-2.0 licensed project GPL compatible by default?
- No. EPL-2.0 licensed projects may explicitly add GPL compatibility by way of adding a Secondary License
# AGPL (Affero General Public License)
- you have to allow the source to be downloaded even if you never distribute the binary but do provide a service
- GPL v2和v3还有一个非常大的“漏洞”，就是软件“发布” 才必须开源。
  - 如果软件不发布，即使使用GPL v2和v3也可以不用开源。
  - 随着以Google为代表的软件作为服务的互联网公司的兴起，它们的“不分发软件，为客户提供网络服务”的商业模式就不受GPL协议的约束
- AGPL = GPL + 一条限制
- 一条限制：如果使用AGPL许可的软件与用户通过网络进行交互，也需要提供源代码给用户，所有的修改也要给用户

- ## [The AGPL License - FOSSA](https://fossa.com/blog/open-source-software-licenses-101-agpl-license/)
- The idea behind the AGPL License was to address the “application service provider (ASP) loophole(漏洞), ”
  - The AGPL License is based on GPL v3. It has the same requirements, plus the statement regarding remote access via a network.
  - Let’s say you create a software program. Another developer takes and modifies it, and then provides access to that modification to paying customers through a software-as-a-service model. 
  - Under the GPL v3, that modification would essentially become proprietary because it wasn’t technically distributed. 
  - Under AGPL, however, that developer would need to make their modified source code available for download.

- Users can change or rework the code, but if they distribute these changes/modifications in any public way (including over a server), they must release these updates in source code form under the AGPL license.
  - As long as these modifications are also released under the GNU AGPL, they can be distributed to others.

- The AGPL License does not permit sublicensing of the code; 
  - that is, you cannot rework or add to the code and then close those changes off to the public. 
  - The “open source-ness” of the original code follows any update or addition. 
  - Both GPL v2 and GPL v3 contain this provision as well.
# Server Side Public License (SSPL)
- [Server Side Public License FAQ](https://www.mongodb.com/licensing/server-side-public-license/faq)
- [Server Side Public License (SSPL) | MongoDB](https://www.mongodb.com/licensing/server-side-public-license)

- ## Why did you base the SSPL on GPL v3 instead of AGPL?
  - The AGPL is a modified version of GPL v3. 
  - The only additional requirement of AGPL is in section 13: if you run a modified program on a server and let other users communicate with it there, you must open source the source code corresponding to your modified version, known as the “Remote Network Interaction” provision of AGPL.
  - 👉🏻 **There is some confusion in the marketplace about the trigger and scope of the Remote Network Interaction provision of AGPL**.
  - As a result, we decided to base the SSPL on GPL v3 and to add a new section 13 which clearly and explicitly sets forth the conditions to offering the licensed program as a third-party service.

- ## What specifically is the difference between the GPL and the SSPL?
  - The only substantive modification is section 13, which makes clear the condition to offering MongoDB as a service. 
  - A company that offers a publicly available MongoDB as a service must release the software it uses to offer such service under the terms of the SSPL, including the management software, user interfaces, application program interfaces, automation software, monitoring software, backup software, storage software and hosting software, all such that a user could run an instance of the service using the source code made available.
# BSD
- ref
  - https://tldrlegal.com/license/bsd-3-clause-license-(revised)
  - https://tldrlegal.com/license/bsd-2-clause-license-(freebsd)

- BSD 2/3-clause license allows you almost unlimited freedom with the software so long as you include the BSD copyright and license notice in it (found in Fulltext). 
- include copyright/license

- 特点
  - 非版权
  - 项目作品适合商业用途
  - 被许可方可以修改工作 
  - 被许可方必须提供引用说明 
  - 被许可方可以根据不同条款重新发布衍生作品 
  - 被许可方不必将其衍生作品和源代码一起发布 
  - 被许可方不得使用原作者名称或商标来为衍生作品背书（3句版和4句版BSD）
  - 被许可方必须在提及此项目功能或用途的所有广告材料中**致谢项目原作者**（4句版BSD）

- 较为宽松，两个变种
  - 要求 协议和版权信息
  - 允许 商用、分发、修改、私用、附加协议
  - 禁止 责任承担
- 可以自由的使用，修改源代码，也可以将修改后的代码作为开源或者专有软件再发布
- 如果再发布的产品中包含源代码，则在源代码中必须带有原来代码中的BSD协议。
- 如果再发布的只是二进制类库/软件，则需要在类库/软件的文档和版权声明中包含原来代码中的BSD协议。
- 不可以用开源代码的作者/机构名字和原来产品的名字做市场推广

- BSD 3-Clause License is a permissive license similar to the BSD 2-Clause License, but with a 3rd clause that prohibits others from using the name of the project or its contributors to promote derived products without written consent(允许、批准).
# EDL(Eclipse Distribution License)
- ref
  - [Eclipse Distribution License v1.0](https://www.eclipse.org/org/documents/edl-v10.php)

- [Is the EDL v1.0 GPL-compatible?](https://opensource.stackexchange.com/questions/10996/is-the-edl-v1-0-gpl-compatible)
  - The Eclipse Distribution License (EDL) is just an alternative name for the BSD 3-clause license, listed by the GNU project as the modified BSD license.
  - This is a highly permissive license that is widely compatible with other licenses, including the GPL and AGPL in all versions.
# MIT
- ref
  - https://www.tldrlegal.com/l/mit

- MIT License (Expat): A short, permissive software license. 
  - Basically, you can do whatever you want as long as you include the original copyright and license notice in any copy of the software/source.  
  - There are many variations of this license in use.
- must include copyright, license

- 特点
  - 非版权
  - 项目作品适合商业用途
  - 被许可方可以修改项目
  - 被许可方必须提供引用说明
  - 被许可方可以根据不同条款重新发布衍生作品
  - 被许可方不必将其衍生作品和源代码一起发布

- 宽松简单且精要的协议
  - 要求 署名作者、协议和版权信息
  - 允许 商用、分发、修改、私用、附加协议
  - 禁止 原作者责任承担
- 和BSD一样宽范的许可协议, 你必须在你的发行版里包含原许可协议的声明，无论你是以二进制发布的还是以源代码发布的
- 被授权人有权利使用、复制、修改、合并、出版发行、散布、再授权及贩售软体及软体的副本。
- 被授权人可根据程式的需要修改授权条款为适当的内容。
- 在软件和软件的所有副本中都必须包含版权声明和许可声明
- 甚至可以用原作者名字来推广
# ISC License
- ref
  - https://tldrlegal.com/license/-isc-license
  - https://choosealicense.com/licenses/isc/

- A short, permissive software license. 
  - Basically, you can do whatever you want as long as you include the original copyright. 
  - This license is functionally **identical to** MIT/Expat and the Simplified BSD licenses, discarding some language that was made unnecessary by the Berne convention.
- must include copyright/license

- The ISC license is functionally equivalent to the BSD 2-Clause and MIT licenses, removing some language that is no longer necessary.
# Common Public Attribution License
- ref
  - https://tldrlegal.com/license/common-public-attribution-license-version-1.0-(cpal-1.0)

- This license is like EPL or MPL, but it has extra requirements that apply even if you use the software as a service (instead of distributing it). 
  - Depending on the notice requirements required by a particular author who releases software under this license, you may need to include the licensor’s logo on splash screens of your software.
# Microsoft Public License (Ms-PL)
- ref
  - https://tldrlegal.com/license/microsoft-public-license-(ms-pl)

- You can do anything you want with the software, so long as you include this license and existing copyrights. 
  - You can only use this with compatible licenses.
- must include copyright/license
# Common Public License 1.0 (CPL-1.0) 
- ref
  - https://tldrlegal.com/license/common-public-license-1.0-(cpl-1.0)

- A precursor to the Eclipse license that is also very explicit in its terms. 
  - This is a weak copyleft license, like MPL and EPL. This is superseded by the Eclipse Public License. 
- must include copyright/license, disclose source
# Free Public License 1.0.0
- ref
  - https://tldrlegal.com/license/free-public-license-1.0.0

- Let anyone do anything as long as they don't hold you liable.
# The Unlicense
- ref
  - https://choosealicense.com/licenses/unlicense/

- A license with no conditions whatsoever which dedicates works to the public domain. 
- Unlicensed works, modifications, and larger works may be distributed under different terms and without source code.
# Universal Permissive License (UPL) 
- ref
  - https://oss.oracle.com/licenses/upl/
  - https://tldrlegal.com/license/universal-permissive-license-1.0-(upl-1.0)

- [graalvm license分析 | mjblog_202009](https://mjblog.github.io/2020/09/25/graal_license/)
  - graalvm社区版本使整体是GPLv2 with classpath exception
  - 目前关心的组件主要有GPLv2(compiler/vm)、UPL(truffle/js)和BSD(sulong)三种协议
  - UPL是非常开放友好的开源协议。不仅允许任意重用代码(包括商业使用)，而且明确提供了专利授权和保护，法律风险非常低

- A highly permissive license **similar to the MIT** License 
  - with added features including an explicit patent grant, clear ability to relicense (to commercial, proprietary, copyleft or etc...) and usable as a CLA.  
  - It is compatible with most commercial and copyleft (GPL-family) licenses.

- The UPL is a highly permissive license, including both copyright and patent licenses, 
  - which permits use and relicensing under both copyleft and commercial terms, and also facilitates use as a contributor license agreement.
- The most important problem the UPL solves is the inclusion of an express patent license in a license 
  - that is both broadly agreed to be uniformly copyleft compatible and also permits the software to be freely used in commercially licensed software (i.e., without concerns about reciprocal license obligations).
  - The MIT and BSD licenses do not include express patent licenses
- Another problem solved with the UPL, is that licensors and distributors are expressly permitted to reference the UPL rather than including a complete copy of the text in each item. 
  - The MIT and BSD licenses expressly require that you include a complete copy of the license in each piece of source code. 
- Finally, the inclusion of the Larger Works concept facilitates use as a contributor license agreement (CLA), 
  - with contributors granting a patent license to the works to which they're contributing, 
  - and therefore creating a common & safe platform for collaboration where no one is going to assert infringement by the same project in which they're an active participant.

- [What is a Universal Permissive License?](https://www.quora.com/What-is-a-Universal-Permissive-License)
  - A Universal Permissive License or UPL is used in software 
    - when you want to release it for free use most of the time you are given up all rights to the software that you developed. 
    - It can be modified to state something like your name must be included as the original developer of the software.

- [Guest View: Use Oracle’s UPL, abandon your intellectual property](https://sdtimes.com/guest-view-use-oracles-upl-abandon-intellectual-property/)
  - (201406)Recently, Oracle submitted the new Universal Permissive License (UPL) for approval to the Open Source Initiative (OSI), claiming the UPL filled the need for 
    - a permissive, MIT-style open-source license with explicit patent grants.
    - Oracle drafted the UPL to address concerns it had with proposed changes to the Java Community Process (JCP), specifically with regard to license rights in others’ reference implementation technology of Java specifications. 
    - Oracle expressed concerns with using other open-source licenses for reference implementation technology due to its need to license this technology under both proprietary licenses (with patent grants) and the GPLv2.
  - At a high level, the UPL copyright and patent licenses are overly broad. 
    - They extend to current and future versions of both the UPL-licensed code as well as any software or hardware identified in a file included with the UPL-licensed code. 
# linkware
- ref
  - [wiki: linkware](https://en.wiktionary.org/wiki/linkware)

- who is using #linkware-license
  - https://github.com/amcharts/amcharts4
    - https://www.amcharts.com/online-store/
    - https://www.amcharts.com/online-store/licenses-explained/
  - https://github.com/DataGridXL/DataGridXL
  - https://github.com/ailon/markerjs2
  - https://icons8.com/license
# Elastic License
- [FAQ on Elastic License 2.0 (ELv2)](https://www.elastic.co/licensing/elastic-license/faq)
- [Elastic License 2.0](https://www.elastic.co/licensing/elastic-license)

- We are moving our Apache 2.0-licensed source code in Elasticsearch and Kibana to be dual licensed under the Elastic License and Server Side Public License (SSPL), giving users the choice of which license to apply.

- The license allows the free right to use, modify, create derivative works, and redistribute, with three simple limitations:
  - You may not provide the products to others as a managed service 
  - You may not circumvent the license key functionality or remove/obscure features protected by license keys
  - You may not remove or obscure any licensing, copyright, or other notices
# Confluent Community License
- [Confluent community license faq](https://www.confluent.io/confluent-community-license-faq/)

- Under the Confluent Community License, you can access the source code and modify or redistribute it; 
  - there is only one thing you cannot do, and that is use it to make a competing SaaS offering. 
  - For example, it does not allow hosting of Confluent ksqlDB, Confluent Schema Registry, Confluent REST Proxy, or other software licensed under the Confluent Community License as online service offerings that compete with Confluent SaaS products or services that provide the same software.  
  - If you are not doing what is excluded, this license change will not affect you.
# Cryptographic Autonomy License
- [Understanding the Cryptographic Autonomy License - Holochain Blog](https://blog.holochain.org/understanding-the-cryptographic-autonomy-license/)
  - Public Performance of Software? 类似歌曲的著作权、表演权
  - TL; DR; Copyleft + Performance
  - Holochain’s license boils down to this: You can run Holochain as free and open source software with a couple of conditions:
  - The source code of Holochain and **any derivative works must be provided under compatible open source terms** which include this condition and the following condition related to privacy of cryptographic keys.
  - You only have permission for “public performance” of Holochain (including use of its APIs for running your dApp) if you preserve each end-user’s privacy and autonomy of their private cryptographic keys.
  - If the privacy of user keys is compromised, then so is the ownership of their data, as well as user’s control of their own copies of the software.
  - I’ve never seen a software license invoke this kind of “public performance” clause, so it may stir up some controversy and make it challenging to get our license accepted by OpenSource.org; but it is the only way we’ve found to release Holochain with responsible protections for end-users.
# data - CDLA(Community Data License Agreement Permissive 2.0)

> aka. CDLA-Permissive-2.0

- refs
  - [Community Data License Agreement Permissive 2.0 | Software Package Data Exchange (SPDX)](https://spdx.org/licenses/CDLA-Permissive-2.0.html)

- [CDLA](https://cdla.dev/)
  - Open source software communities have shown the power of open collaboration building some of the world’s most important software assets together. 
  - There are communities also looking to collaboratively build datasets that can be shared and developed in a very similar model to software.
  - The challenge is that intellectual property systems around the world treat data differently than software. 
  - In June 2021, we released the CDLA-Permissive-2.0

- [规范使用开源数据集，一定要看License - 知乎](https://zhuanlan.zhihu.com/p/544854011)
  - 常用的数据集许可协议有3种来源
  - 知识共享 (CC)
    - 主要涉及4项权利，署名（BY）权，传染（SA-shareAlike）权，非盈利（NC）权，禁止演绎（ND）权。
    - 知识共享组织于2009年发布了一种放弃著作权的便捷方式，即CC0。严格来讲CC0并非双方的许可合同，而是一种单方的声明。选择CC0作为许可协议，则说明作者将数据集捐赠给公众使用，此数据集完全公有，使用时无需署名，也无其他限制
  - 开放数据共享 (ODC)
    - 为开放数据提供合法工具，他们提供三种许可类型
    - ODC-PDDL: 版权所有者永久删除所有版权，不保留任何权利。这对应于CC0 许可协议。
    - ODC-BY: 你可以自由分享和改编，但需要注明出处，允许商业用途。这对应于CC BY（署名）许可。
    - ODC-ODbL: 你可以自由分享和改编，并在基于原作创作的新作品适用同类型的许可协议。允许商业用途。这对应于CC BY-SA (署名-相同方式共享)许可协议。
  - 社区数据许可协议 (CDLA)
    - CDLA-Permissive-2.0: 对开放数据的贡献者和使用者不作要求。你可以使用、修改和共享，许可协议不对结果的使用、修改或共享施加任何限制或义务。
    - CDLA-Sharing-1.0: 这属于copyleft（强制共享）许可类别，你可以使用、修改和共享，但无论是否修改，基于原作创作的新作品必须与原始版本有相同的许可协议。
# relicense-known
- [Grafana, Loki, and Tempo will be relicensed to AGPLv3_202104](https://grafana.com/blog/2021/04/20/grafana-loki-tempo-relicensing-to-agplv3/)
  - Over the last few years, we’ve watched closely as almost every at-scale open source company that we admire (such as Elastic, Redis Labs, MongoDB, Timescale, Cockroach Labs, and many others) has evolved their license regime. 
  - In almost all of these cases, the result has been a move to a non-OSI-approved source-available license.
