---
title: wiki-license-open-source-code
tags: [law, license, open-source]
created: '2020-07-13T03:29:04.214Z'
modified: '2021-09-14T18:58:58.275Z'
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

- ref
  - https://tldrlegal.com/
  - https://choosealicense.com/licenses/
  - linkware, watermark

# pieces

- Copyright”指软件的版权和其它一切权利归软件作者所私有，用户只有使用权，没有其它如复制、重新修改发布等权利。
- 而“Copyleft”的特点是仅有版权归原作者所有，其他一切权利可以与任何人共享。
  - “Copyleft”通常被译作“著佐权”，即通过许可证的形式，补足、辅佐著作权（Copyright）不足的版权授权，相当于一种权利与义务的契约

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
  - https://tldrlegal.com/license/gnu-lesser-general-public-license-v3-(lgpl-3)

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

# AGPL (Affero General Public License)

- you have to allow the source to be downloaded even if you never distribute the binary but do provide a service
- GPL v2和v3还有一个非常大的“漏洞”，就是软件“发布” 才必须开源。
  - 如果软件不发布，即使使用GPL v2和v3也可以不用开源。
  - 随着以Google为代表的软件作为服务的互联网公司的兴起，它们的“不分发软件，为客户提供网络服务”的商业模式就不受GPL协议的约束
- AGPL = GPL + 一条限制
- 一条限制：如果使用AGPL许可的软件与用户通过网络进行交互，也需要提供源代码给用户，所有的修改也要给用户

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

# MPL (Mozilla Public License)

- ref
  - https://tldrlegal.com/license/mozilla-public-license-2.0-(mpl-2)

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

- BSD协议和GPL协议的折衷点
  - 要求 公开源码、协议和版权信息
  - 允许 商用、分发、修改、专利授权、私用、附加协议
  - 禁止 责任承担、商标使用
- MPL虽然要求对于经MPL许可证发布的源代码的修改也要以MPL许可证的方式再许可出来，以保证其他人可以在MPL的条款下共享源代码。
  - 但是，在MPL许可证中对“发布”的定义是“以源代码方式发布的文件”，这就意味着MPL允许一个企业在自己已有的源代码库上加一个接口，除了接口程序的源代码以MPL许可证的形式对外许可外，源代码库中的源代码就可以不用MPL许可证的方式强制对外许可。
  - 这些，就为借鉴别人的源代码用做自己商业软件开发的行为留了一个方式
- MPL许可证第三条第7款中允许被许可人将经过MPL许可证获得的源代码同自己其他类型的代码混合得到自己的软件程序。
- 要求源代码的提供者不能提供已经受专利保护的源代码
- 要求所有再发布者都得有一个专门的文件就对源代码程序修改的时间和修改的方式有描述
- MPL 2.0与Apache许可证以及GPL第二版或更新、LGPL2.1版或更新，及AGPL第三版或更新兼容。而1.1版因为有“一些复杂的限制”造成与GPL的不兼容（从而阻止升级到MPL 2.0）

- ## [How does the scope of the MPL's copyleft compare with the LGPL and GPL's copyleft?](https://www.mozilla.org/en-US/MPL/2.0/FAQ/)
- MPL: The copyleft applies to any files containing MPLed code.
- GPL: The copyleft applies to all software based on GPLed code.
- LGPL: The copyleft applies to any library based on LGPLed code.

- ## I want to use software which is available under the MPL. What do I have to do?
- Nothing. 
- Like all other free and open source software, software available under the MPL is available for anyone (including individuals and companies) to use for any purpose. 
- The MPL only creates obligations for you if you want to distribute the software outside your organization.

- ## I want to distribute (outside my organization) executable programs or libraries that I have compiled from someone else's unchanged MPL-licensed source code, either standalone or part of a larger work. 
- You must inform the recipients where they can get the source for the MPLed code in the executable program or library you are distributing (i.e., you must comply with Section 3.2). 
- You may distribute any executables you create under a license of your choosing, as long as that license does not interfere with the recipients' rights to the source under the terms of the MPL.

- ## I want to distribute (outside my organization) MPL-licensed source code that I have modified. 
- You must inform the recipients that the source code is made available to them under the terms of the MPL (Section 3.1), including any Modifications (as defined in Section 1.10) that you have created.
- You must respect the restrictions on removing or altering notices in the source code

- ## I want to distribute (outside my organization) an executable program based on MPL-licensed source code that I have modified. What do I have to do?
- You must make available the MPL-licensed portions of the source code as described in the previous question, and inform the recipients how they can obtain such source code

- ## If I use MPL-licensed code in my proprietary application, will I have to give all the source code away?
- No. The license requires that Modifications (as defined in Section 1.10 of the license) must be licensed under the MPL and made available to anyone to whom you distribute the Source Code. 
- However, new files containing no MPL-licensed code are not Modifications, and therefore do not need to be distributed under the terms of the MPL, even if you create a Larger Work (as defined in Section 1.7) by using, compiling, or distributing the non-MPL files together with MPL-licensed files. 
- This allows, for example, programs using MPL-licensed code to be statically linked to and distributed as part of a larger proprietary piece of software, which would not generally be possible under the terms of stronger copyleft licenses.

# EPL (Eclipse Public License)

- ref
  - https://tldrlegal.com/license/eclipse-public-license-1.0-(epl-1.0)
  - https://www.eclipse.org/legal/epl-2.0/faq.php

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
- EPL 1.0
  - 允许Recipients任意使用、复制、分发、传播、展示、修改以及改后闭源的二次商业发布
  - 当一个Contributors将源码的整体或部分再次开源发布的时候, 必须继续遵循EPL开源协议来发布, 而不能改用其他协议发布
  - 商业软件可以使用，也可以修改EPL协议的代码，但要承担代码产生的侵权责任
- What are the major changes between EPL-1.0 and EPL-2.0?
  - The term of art is now referred to as "file" rather than "module"; 
  - The choice of law provisions has been removed; 
  - The license is now suitable for scripting languages such as JavaScript; and
  - The license now includes an option to add a secondary license for GPL-2.0+ compatibility.
- EPLv1 is copyleft, because it requires you to release any changes you made to the EPL code while working on your main app. 
  - The difference from GPL is that it's a commercial-friendly copyleft, requiring you only to make those changes available and only if you distribute your commercial app. 
  - And if you made no changes, no source code to release

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

- A highly permissive license similar to the MIT License 
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

- who is using
  - https://github.com/amcharts/amcharts4
    - https://www.amcharts.com/online-store/
    - https://www.amcharts.com/online-store/licenses-explained/
  - https://github.com/DataGridXL/DataGridXL
  - https://github.com/ailon/markerjs2
  - https://icons8.com/license
