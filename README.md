
# 前言

    互联网产品信息无障碍是指，互联网产品可以被视障者等用户顺畅使用，也指任何人（无论健全人还是残障群体，无论是年轻人还是老年人）都能访问、理解、操作互联网产品，并能顺畅使用互联网产品，而不论用户使用何种设备配置、网络连接方式、浏览工具和上网辅助技术。互联网产品是网络信息的载体，互联网产品信息无障碍优化主要涉及互联网产品的无障碍设计、开发、改造。互联网产品信息无障碍设计以通用设计思想为指导，强调用户体验，针对各类人群（特别是残障群体和老年人）在使用互联网过程中存在的障碍进行设计，以可访问性、易用性为设计准则，并且在互联网产品设计开发中严格遵守互联网产品信息无障碍标准。
    国内的互联网信息无障碍标准是由中华人民共和国工业和信息化部主持撰写，服务于身体机能差异人群、基础环境差异人群、文化环境差异人群、行为习惯差异人群，目的是为残障群体、有特殊需求的健全人无障碍的获取网络上的信息，互联网信息无障碍系列标准有《信息无障碍 身体机能差异人群 网站设计无障碍技术要求》(YD/T 1761-2008)、《信息无障碍 身体机能差异人群 网站无障碍评级测试方法》(YD/T 1822 -2008)、《信息无障碍 语音上网技术要求》(YD/T 2098-2010)、《信息无障碍 用于身体机能差异人群的通信终端设备设计导则》(YD/T 2065-2009)、《信息终端设备信息无障碍辅助技术的要求和评测方法》 （YD/T 1890-2009)，在互联网产品设计、评测、语音上网等方面指导互联网信息无障碍产品的开发。
    W3C作为互联网技术领域最具权威和影响力的国际中立性技术标准机构，在互联网领域建立了许多标准，本文介绍的互联网标准有W3C中WAI组织的Web内容无障碍指南 (WCAG2.0)，还有谷歌公司的android信息无障碍 开发指南与苹果公司的iOS信息无障碍开发指南。
    WCAG2.0定义了如何让残障群体方便使用Web内容的方法。涉及广泛的残障类别包括视觉、听觉、身体、言语、认知、学习以及神经残疾。指南包括整体原则、一般准则、可测试成功标准、充分性技巧和建议性技巧，并为记录在案的常见错误提供了丰富的例子，资源链接及代码。整体性原则包括四大原则，是Web无障碍的基础，具体包括可感知性、可操作性、可理解性和稳定性。每个原则包含12个准则，最终为了实现让不同残障用户更容易的访问Web。这些准则是不可测试的，WCAG2.0提供了框架和总体目标，以帮助开发者了解成功标准和更好地实现该原则。对于每一个准则，WCAG2.0提供了可测试的成功标准，可用在需求和一致性测试的地方，例如设计规范、采购、管理、合同协议。为了满足不同群体的不同需求，WCAG2.0定义了一致性的三个级别：A(最低)、AA、AAA(最高)。对于每条准则和成功标准，WCAG2.0说明了范围广泛的各种技巧。该技巧为告知性的，且分为两类：充分达到成功标准的技巧和建议性技巧。建议性技巧超越了成功标准的范围，是为了让开发者更好的理解这些准则。一些建设性技巧解决了一些障碍，这些障碍在可测试的成功标准里没有覆盖到。凡是已知的常见失败，都已记录在案。
    根据WCAG2.0，为了实现互联网产品信息无障碍优化，应该重视人机交互的操作技术与工具型产品的开发与应用关键技术研究与应用开发，以实现视、听、语、触功能障碍人群的操作行为向现行计算机系统和网络系统的规范操作模式的转换。尤其是大力推进视障读屏软件的开发、应用、优化与创新，帮助视障用户独立地操作计算机。除此之外，盲用网页定位导航辅助装置开发应用及普及也是一个重要的改造方向，开发“盲用网络页面定位导航辅助装置”，导引视障者完成网页搜索和定位选择功能。在开发中，开发团队对信息无障碍优化的重视程度，直接影响到产品的信息无障碍程度。在开发中应该注意的问题有：
    1)开发团队成员需要对产品所在平台的无障碍方面的编码使用有所了解，每个平台有不同的无障碍属性的编码及API，可通过其网站查询学习到相关资料；常用的网页和移动端产品的无障碍开发标准有Web内容无障碍指南 (WCAG) 2.0、iOS无障碍开发指南、安卓无障碍开发指南；
    2)尽量避免只有单一反馈或只允许单一反馈的功能实现（如验证码只有视觉形式）；
    3)产品界面在满足功能实现的前提下，应尽量具有较强的逻辑关系，简明、易懂、清晰；
    4)参考国内外关于通用设计和无障碍交互设计的相关指南、建议；
    5)采用以焦点为基础的页面布局，保证不同的用户可以通过不同的输入设备（键盘、鼠标、轨迹球、手势等）对产品所包含的控件元素进行操作；
    6)注意控件焦点设置的大小及排列顺序，以便用户可以清楚地获取焦点位置，了解产品界面布局及功能逻辑；
    7)应尽量使用系统内置的标准控件，若产品中使用了自定义控件，应为该控件设置可以匹配的无障碍接口及控件描述；
    8)注意对非装饰性图片控件添加描述，该描述应简明易懂、准确；
    9)尽量使用系统平台的标准无障碍功能接口（辅助功能接口），避免使用独立的无障碍功能实现方案；
    10)若遇到功能本身的实现与无障碍实现冲突时，应考虑是否有其他的解决方案，避免直接放弃实现无障碍的做法；
    11)大部分的控件需要的无障碍属性是类似的，开发过程中应注意总结归纳，形成较为标准的实施方式；
    12)对于产品所在系统平台的辅助功能或无障碍接口有持续关注，并及时更新、提高相关技术；
    13)将无障碍相关编码纳入功能实现规范中，在每个产品版本中持续考虑同一功能的无障碍问题，避免出现产品无障碍体验倒退的情况。
    本书从web端与移动端的无障碍问题入手，描述了常见的无障碍问题及其可能的原因，并针对相应的无障碍问题给出解决建议。

# 本书结构

    本书包括前言、web端无障碍问题、移动端无障碍问题三部分，前言是对互联网信息无障碍概念、国内的无障碍标准、WCAG2.0进行简单介绍，并列举了常见的无障碍问题。
    web端无障碍问题包括三部分：web常见控件的无障碍问题、web常见应用的无障碍问题、web无障碍建议；控件部分包含13个控件，每个控件有2-10条问题，每个问题包含问题描述、可能原因、修改建议三部分；问题描述是对问题进行简单描述，方便开发者理解问题；可能原因是造成这种问题出现的可能的原因；修改建议是针对问题和原因，我方提出的建议性的修改方案，因技术原因，部分问题的修改建议为空，待补充。
    Web部分功能的无障碍问题部分包含4个功能的问题，每个功能包含3-6个问题，每个问题包含问题描述、可能原因、修改建议、参考资料四部分；问题描述是对问题进行简单描述，方便开发者理解；可能原因、修改建议因技术限制，置空，待补充；参考资料是针对每个问题，给出的参考性的建议与样例，可用来解决问题。
    web无障碍建议部分包含10个方面的内容，这些内容来自WCAG2.0支持文档--怎样满足WCAG2.0，为Web开发者提供无障碍参考。
    移动端无障碍问题部分包含android无障碍指南、ios无障碍指南、移动端无障碍问题三个部分；android无障碍指南参考自https://developer.android.com/guide/topics/ui/accessibility/index.html，包含9个章节，为android开发者提供无障碍参考；ios无障碍指南内容参考自https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/iPhoneAccessibility/Introduction/Introduction.html），包含10个章节的内容，为ios开发者提供无障碍参考；
    移动端问题部分常见控件的无障碍问题、常见工程的无障碍问题，常见控件的无障碍问题包括13个控件的无障碍问题，每个控件包含2-7个无障碍问题，每个无障碍问题包含问题描述、可能原因、修改建议三个部分；问题描述是对无障碍问题进行简单描述，方便开发者理解；可能原因与修改建议部分，只有部分给出，待审查与补充。常见功能的无障碍问题包含3个功能，每个功能包含2-6个问题，每个问题包含问题描述、可能原因、修改建议三部分：问题描述是对无障碍问题进行简单描述，方便开发者理解。可能原因和修改建议待补充。