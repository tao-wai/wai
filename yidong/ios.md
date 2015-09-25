
# （二）ios无障碍指南


    参考来源：https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/iPhoneAccessibility/Introduction/Introduction.html）


## 1.IOS无障碍特性与VoiceOver


    VoiceOver 是苹果公司创新的读屏技术，通过这个技术，用户无需看屏幕就可以控制设备。VoiceOver在用户界面与用户触控之间充当媒介，描述了应用程序中的元素与行为。当VoiceOver激活时，用户无需担心意外地删除了联系人或者拨打了电话，因为VoiceOver会提醒用户界面位置，他们可以操作什么，结果如何。
    一个程序是不是无障碍的，取决于用户可以交互的所有界面元素是否是无障碍的。一个界面元素是否是无障碍的取决于它是否在恰当的时候告知用户它是一个无障碍的元素。
    一个无障碍的界面元素必须准确提供关于它的信息才能被使用。这些信息包括它在屏幕的位置、名称、行为、值和类型。这正是VoiceOver播报给用户的信息。iOS SDK包含了编程接口和工具，来帮你确保程序中的用户界面元素是无障碍且好用的。
    应该让iPhone应用能被VoiceOver的用户们无障碍的使用，因为：
    这会增加你的用户基数。你已经努力的创造优秀的程序，不要错过让你的程序能被更多用户使用的机会。
    无障碍应用可以使你的用户无需看屏幕。视障用户可以通过VoiceOver的帮助来使用的你的应用。
    写无障碍程序使你理解无障碍准则。很多管理部门编写了无障碍准则，你为VoiceOver用户编写无障碍的iPhone应用能帮助你满足这些准则。
    这是正确的决定。
    支持无障碍特性不会影响你创造优异iPhone应用的能力，记得这点非常重要。为用户界面编程接口增加薄薄的一个功能层，不会改变应用的外观，也不会妨碍到应用的主要逻辑。

## 2.IOS UI无障碍编程接口


    UI无障碍编程接口包含两个非正式协议，一个类，一个函数，还有一些常量。
    UIAccessibility非正式协议。实现UIAccessibility协议的对象可以报告无障碍状态（即他们是否是无障碍的）并且提供关于他们的描述性信息。UIAccessibility协议默认由标准UIKit控件和视图实现。
    UIAccessibilityContainer非正式协议。此协议通过子类UIView来使它所包含的部分或者全部对象是无障碍的分离元素，当非UIView子类的对象被UIView视图包含时，这些元素不会自动变成无障碍元素，此时UIAccessibilityContainer协议就非常有用。
    UIAccessibilityElement类。定义了一个对象是否能通过UIAccessibilityContainer协议返回。你可以创建UIAccessibilityElement实例来代表无法自动变为无障碍的元素，例如一个没有继承自UIView的对象，或者一个不存在的对象。
    UIAccessibilityConstants.h头文件。此头文件定义了用来描述某些特征的常量。这些常量即可展示的无障碍元素，还有可被应用发布的通知。


## 3.UI无障碍(UIAccessibility)


    文档来源：https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibility_Protocol/#//apple_ref/c/data/UIAccessibilityAnnouncementNotification

    UI无障碍非正式协议提供了应用界面元素的无障碍信息。辅助应用，比方说voiceover，将信息传递残障用户来帮助用户使用应用。
    标准UIKit控件和视图实现了UIAccessibility方法，因此默认支持辅助应用。这意味着如果应用只使用标准控件和视图，例如UIButton，UISegmentedControl和 UITableView，只需要当默认值不完整的时候提供特定应用的详细信息。可以在Interface     Builder中或者该非正式协议中设置这些值。
    UIAccessibility非正式协议也可以被通过     UIAccessibilityElement类来实现，这个类可以显示自定义用户界面对象。如果创建一个完全的自定义UIView子类，可能需要去创建 UIAccessibilityElement的一个实例来显示它。在这种情况下，应该支持所有UIAccessibility属性来正确的设置和返回无障碍元素的属性。

### 3.1无障碍判定


    isAccessibilityElement
    是一个布尔值，决定该元素是不是一个辅助技术可以访问的无障碍元素。该属性的默认值为NO，除非接收器是一个标准UIKit控件，值为YES。
    辅助技术可以获得无障碍元素呈现的信息。因此，如果实现一个自定义控件或者视图，应该对残障用户无障碍，应该设置这个属性为YES。唯一例外的是，一个只为其他无障碍条目提供容器的，这样的视图应该实现UIAccessibilityContainer协议并设置该属性为NO。
    声明：
    SWIFT
    var isAccessibilityElement: Bool
    OBJECTIVE-C
    @property(nonatomic) BOOL isAccessibilityElement
    版本：Available in iOS 3.0 and later.

### 3.2配置无障碍元素


    accessibilityActivationPoint
    在屏幕坐标上，无障碍元素可激活的点；此属性的默认值是无障碍元素框架的中点，是由accessibilityFrame提供的。一个元素的活跃点是当用户双击该元素时，voiceover激活的特定区域。
    指定一个活跃点的能力允许一个元素在不同的情况下呈现给voiceover不同的点，而不是改变元素自己的视觉显示，例如，一个主屏幕app图标的标准活跃点是图标的中点，但是当用户在主屏幕上重现安排图标时，活跃点更改为删除控件的中点（即，在图标左上角的圆圈X）。
    可以使用这个属性来保证一个小元素的活跃点保持精确，尽管呈现给voiceover的是个大版本。
    声明:
    SWIFT
    var accessibilityActivationPoint: CGPoint
    OBJECTIVE-C
    @property(nonatomic) CGPoint accessibilityActivationPoint
    版本：Available in iOS 5.0 and later.

    accessibilityElementsHidden
    是一个布尔值，指明一个无障碍元素内部的无障碍元素是不是隐藏的；这个属性的默认值是No。可能会使用该属性去隐藏视图，这些视图被新来的视图覆盖。在此案例中，隐藏视图仍然是可见的，但是他们不是用户行为的焦点。
    可能使用这个属性来隐藏一个短暂的视图，而voiceover用户不会注意到。例如，voiceover不需要去描述透明视图，这些视图当用户调整设备上的音量的时候才会出现，因为这个动作的听觉反馈是足够的。
    声明：
    SWIFT
    var accessibilityElementsHidden: Bool
    OBJECTIVE-C
    @property(nonatomic) BOOL accessibilityElementsHidden
    版本：Available in iOS 5.0 and later.

    accessibilityFrame
    在屏幕坐标上，无障碍元素的框架；这个属性的默认值是CGRectZero，除非接收器是一个UIView对象或者是一个UIView的子类，这种情况，属性值为视图的框架。
    一个无障碍元素呈现一个非UIView子类的对象应该设置该属性，因为这类对象的屏幕坐标不是已知的。
    声明：
    SWIFT
    var accessibilityFrame: CGRect
    OBJECTIVE-C
    @property(nonatomic) CGRect accessibilityFrame
    版本：
    Available in iOS 3.0 and later.

    accessibilityHint
    用本地语言简单描述无障碍元素的行为结果；这个属性的默认值是nil，除非接收器是一个UIKit控件，这种情况下，系统根据控件类型自动提供hint。
    当在一个无障碍元素上执行一个操作，且根据无障碍label不能得到明显的结果时，一个无障碍hint帮助用户理解执行结果。例如，提供一个add按钮在应用中，按钮的无障碍标签帮助用户理解，在应用中点击这个按钮会增加值。如果，另一方面，你的应用允许用户通过点击一个列表中歌曲的名字来播放歌曲，列表的无障碍标签不会告诉用户这个。帮助辅助应用为残障用户提供信息，列表适当的hint应该为“播放歌曲”。
    以下为为一个无障碍元素传感爱你hint的准则：
    hint应该是一个非常简短的短语，且以动词开头，名词结尾。例如“播放歌曲”或“购买项目”。
    避免开头的动词的使用祈使语气，因为这可能会听起来想命令。
    不要重复的提示操作类型。例如，不要创建这样的提示，如“点击去播放的歌曲”或“点击播放这首歌。”
    不要重复提示控件或视图类型。例如，不要创建这样的提示，如“播放该行中的歌曲”或“增加了一个联系人姓名按钮。”
    声明：
    SWIFT
    var accessibilityHint: String?
    OBJECTIVE-C
    @property(nonatomic, copy, nullable) NSString *accessibilityHint
    版本：Available in iOS 3.0 and later.

    accessibilityLabel
    用本地语言简洁标签定义无障碍元素；这个属性的默认值为nil，除非接收器是个UIKit控件，这种情况下自动派生控件的label。
    注意：如果在一个UISegmentedControl中提供一个UIImage对象，可以设置每个图片的这个属性来保证该部分可以正常访问。
    如果实现一个自定义控件和视图，或者在UIKit空间上显示一个自定义图标，应该设置这个属性来保证无障碍元素有合适的label。如果一个无障碍元素不显示一个描述label，这个属性应该是简短的、本地化的指明该元素的label。例如，一个“播放音乐”的按钮可能会为近视用户显示该按钮是做什么的。为了可访问性，按钮应该有无障碍；label“播放”“播放音乐”，这样辅助应用可以提供这些信息给残障用户。注意，但是，label应该永远不包括控件类型因为类型信息被包含在与无障碍元素有关的特性中。
    声明：
    SWIFT
    var accessibilityLabel: String?
    OBJECTIVE-C
    @property(nonatomic, copy, nullable) NSString *accessibilityLabel
    版本：Available in iOS 3.0 and later.

    accessibilityLanguage
    读出label、hint、value值的语言；此属性的默认值是nil，如果没有语言设置，会使用用户当前的语言。
    如果需要设置这个属性，保证使用一种语言的ID标签，格式需要遵循BCP47规范。这个规范的草图在http://www.rfc-editor.org/.
    声明：
    SWIFT
    var accessibilityLanguage: String?
    OBJECTIVE-C
    @property(nonatomic, strong, nullable) NSString *accessibilityLanguage
    版本：Available in iOS 4.0 and later.

    accessibilityPath
    在屏幕坐标上，一个元素的路径；该属性的默认值为nil，如果没有路径设置，无障碍框架矩形被用来突出元素。
    当为一个属性指定一个值，辅助技术使用path对象来突出元素。
    声明：
    SWIFT
    @NSCopying var accessibilityPath: UIBezierPath?
    OBJECTIVE-C
    @property(nonatomic, copy, nullable) UIBezierPath *accessibilityPath
    版本：Available in iOS 7.0 and later.

    accessibilityTraits
    无障碍特性的组合能最好的展现无障碍元素的特性；该属性的默认为UIAccessibilityTraitNone ，除非接收器是一个UIKit控件，这种情况下，该属性的值应该与该控件有关的标准trait设置。
    如果实现一个自定义控件和视图，需要去选择所有的最佳描述对象的无障碍特性，且通过执行一个OR操作，使用父类特性将这些特性组合(换句话说，使用super.accessibilityTraits).详见Accessibility Traits。
    声明：
    SWIFT
    var accessibilityTraits: UIAccessibilityTraits
    OBJECTIVE-C
    @property(nonatomic) UIAccessibilityTraits accessibilityTraits
    版本：Available in iOS 3.0 and later.

    accessibilityValue
    一个无障碍元素的value；此属性的默认值为nil，除非接收器为一个UIKit控件，这种情况下该属性呈现的是控件的值，当值与label不同的时候。
    当一个无障碍元素有一个静态label，和一个动态值，应该设置这个属性来返回值。例如，虽然一个无障碍元素有一个“信息”label，它的值是当前文本域内的文本。
    声明：
    SWIFT
    var accessibilityValue: String?
    OBJECTIVE-C
    @property(nonatomic, copy, nullable) NSString *accessibilityValue
    版本：Available in iOS 3.0 and later.

    accessibilityViewIsModal
    一个布尔值，用来指明视图内的无障碍元素是否应该被voiceover忽略，这些视图是接收器的兄弟；该属性的默认值为NO。当该属性的值为YES时，voiceover忽略接收视图的兄弟视图中的元素。
    例如，一个窗口包含兄弟视图A和B，设置B的accessibilityViewIsModal为YES，voiceover会忽略A元素。另一方面，如果视图B包含一个子视图C，且设置C的accessibilityViewIsModal为YES，voiceover不会忽略A中的元素。
    声明：
    SWIFT
    var accessibilityViewIsModal: Bool
    OBJECTIVE-C
    @property(nonatomic) BOOL accessibilityViewIsModal
    版本：Available in iOS 5.0 and later.

    shouldGroupAccessibilityChildren
    一个布尔值，用来指明voiceover是否应该将接收器子元素组合在一起讲述，无论这些子元素位于屏幕上的哪个位置；该属性的默认值为NO。
    例如，假设一个垂直展示条目的app。正常的，voiceover会通过水平方向导航这些元素。在垂直列项里的条目父级视图中，设置这个属性为YES，voiceover会尊重app的分组且正确定位它们。
    声明：
    SWIFT
    var shouldGroupAccessibilityChildren: Bool
    OBJECTIVE-C
    @property(nonatomic) BOOL shouldGroupAccessibilityChildren
    版本：Available in iOS 6.0 and later.
    
    accessibilityNavigationStyle
    应用于对象和它的元素的导航方式。一些辅助技术让用户选择一个父级视图和容器，为了导航自己的元素。这个属性控制行为是不是应用于当前对象。开关控件使用这个技术，但是voiceover和其他辅助技术不使用。
    这个属性的默认值为UIAccessibilityNavigationStyleAutomatic。
    声明：
    SWIFT
    var accessibilityNavigationStyle: UIAccessibilityNavigationStyle
    OBJECTIVE-C
    @property(nonatomic) UIAccessibilityNavigationStyle accessibilityNavigationStyle
    版本：Available in iOS 8.0 and later.


### 3.3数据类型
    UIAccessibilityTraits
    包含无障碍特性的组合掩码，这些无障碍特性最能描述一个无障碍元素；
    声明：
    SWIFT
    typealias UIAccessibilityTraits = UInt64
    OBJECTIVE-C
    typedef uint64_t UIAccessibilityTraits;
    引入声明
    OBJECTIVE-C
    @import UIKit;
    SWIFT
    import UIKit
    版本：Available in iOS 3.0 and later.
    
    UIAccessibilityZoomType
    可以生效的系统缩放的类型；
    声明：
    SWIFT
    enum UIAccessibilityZoomType : Int {
        case InsertionPoint
    }
    OBJECTIVE-C
    typedef enum {
       UIAccessibilityZoomTypeInsertionPoint,
    } UIAccessibilityZoomType;
    常量：
    UIAccessibilityZoomTypeInsertionPoint ：系统缩放类型是文本插入点。Available in iOS 5.0 and later.
    引入声明：
    OBJECTIVE-C
    @import UIKit;
    SWIFT
    import UIKit
    版本：Available in iOS 5.0 and later.
    
    UIAccessibilityNotifications
    一个无障碍应用可以发送的通知；
    声明：
    SWIFT
    typealias UIAccessibilityNotifications = UInt32
    OBJECTIVE-C
    typedef uint32_t UIAccessibilityNotifications;
    引入声明：
    OBJECTIVE-C
    @import UIKit;
    SWIFT
    import UIKit
    版本：Available in iOS 3.0 and later.


### 3.4常量


    Accessibility Traits
    无障碍特性可以告知辅助应用无障碍元素怎样行动或者怎样被对待。
    声明：
    SWIFT
    var UIAccessibilityTraitNone: UIAccessibilityTraits
    var UIAccessibilityTraitButton: UIAccessibilityTraits
    var UIAccessibilityTraitLink: UIAccessibilityTraits
    var UIAccessibilityTraitSearchField: UIAccessibilityTraits
    var UIAccessibilityTraitImage: UIAccessibilityTraits
    var UIAccessibilityTraitSelected: UIAccessibilityTraits
    var UIAccessibilityTraitPlaysSound: UIAccessibilityTraits
    var UIAccessibilityTraitKeyboardKey: UIAccessibilityTraits
    var UIAccessibilityTraitStaticText: UIAccessibilityTraits
    var UIAccessibilityTraitSummaryElement: UIAccessibilityTraits
    var UIAccessibilityTraitNotEnabled: UIAccessibilityTraits
    var UIAccessibilityTraitUpdatesFrequently: UIAccessibilityTraits
    var UIAccessibilityTraitStartsMediaSession: UIAccessibilityTraits
    var UIAccessibilityTraitAdjustable: UIAccessibilityTraits
    var UIAccessibilityTraitAllowsDirectInteraction: UIAccessibilityTraits
    var UIAccessibilityTraitCausesPageTurn: UIAccessibilityTraits
    var UIAccessibilityTraitHeader: UIAccessibilityTraits
    OBJECTIVE-C
    UIAccessibilityTraits UIAccessibilityTraitNone;
    UIAccessibilityTraits UIAccessibilityTraitButton;
    UIAccessibilityTraits UIAccessibilityTraitLink;
    UIAccessibilityTraits UIAccessibilityTraitSearchField;
    UIAccessibilityTraits UIAccessibilityTraitImage;
    UIAccessibilityTraits UIAccessibilityTraitSelected;
    UIAccessibilityTraits UIAccessibilityTraitPlaysSound;
    UIAccessibilityTraits UIAccessibilityTraitKeyboardKey;
    UIAccessibilityTraits UIAccessibilityTraitStaticText;
    UIAccessibilityTraits UIAccessibilityTraitSummaryElement;
    UIAccessibilityTraits UIAccessibilityTraitNotEnabled;
    UIAccessibilityTraits UIAccessibilityTraitUpdatesFrequently;
    UIAccessibilityTraits UIAccessibilityTraitStartsMediaSession;
    UIAccessibilityTraits UIAccessibilityTraitAdjustable;
    UIAccessibilityTraits UIAccessibilityTraitAllowsDirectInteraction;
    UIAccessibilityTraits UIAccessibilityTraitCausesPageTurn;
    UIAccessibilityTraits UIAccessibilityTraitHeader;
    常量：
    UIAccessibilityTraitNone ：无障碍元素无特性；Available in iOS 3.0 and later.
    UIAccessibilityTraitButton ：无障碍元素应该被当做button；Available in iOS 3.0 and later.
    UIAccessibilityTraitLink ：无障碍元素应被当做link；Available in iOS 3.0 and later.
    UIAccessibilityTraitSearchField ：无障碍元素应被当做一个搜索区域；Available in iOS 3.0 and later.
    UIAccessibilityTraitImage ：无障碍元素应该被当做一个图片，这个特性可以与button和link特性。Available in iOS 3.0 and later.
    UIAccessibilityTraitSelected ：无障碍元素是当前选择的。可以使用这个特性去描述无障碍元素，例如在已选择表行或者选择控件中的选择片段。Available in iOS 3.0 and later.
    UIAccessibilityTraitPlaysSound ：当元素被激活时，无障碍元素有自己声音。Available in iOS 3.0 and later.
    UIAccessibilityTraitKeyboardKey ：无障碍元素的行为想一个键盘键。Available in iOS 3.0 and later.
    UIAccessibilityTraitStaticText ：被当做不能改变的静态文本的无障碍元素。Available in iOS 3.0 and later.
    UIAccessibilityTraitSummaryElement ：当应用启动的时候无障碍元素提供总结信息，可以使用这个特性描述无障碍元素，这个无障碍元素提供当前位置、设置、状态的信息，比如天气应用中的当前气温。Available in iOS 3.0 and later.
    UIAccessibilityTraitNotEnabled ：无障碍元素不能使用且不能响应用户交互。Available in iOS 3.0 and later.
    UIAccessibilityTraitUpdatesFrequently ：无障碍元素频繁刷新label和value。可以使用这个元素来描述无障碍元素，这个元素的label或value频繁发送刷新通知来刷新。当想要辅助应用避免处理持续通知，相反的，当需要刷新信息的时候调查变更时，包含该特性。例如，可能需要这个特性去描述一个秒表的读出。Available in iOS 3.0 and later.
    UIAccessibilityTraitStartsMediaSession ：当被激活时，无障碍元素开启一个多媒体会话。可以使用这个特性来暂停辅助技术的音频输出，比如，voiceover不应该打断多媒体会话。例如，可能使用这个特性来暂停voiceover讲话，当用户录音的时候。Available in iOS 4.0 and later.
    UIAccessibilityTraitAdjustable ：通过一定范围的值，无障碍元素可连续调节。可以使用这个特性来描述无障碍元素，这个元素用户可以使用连续的方式调整，例如一个滑块或者选择器视图。如果你指定该元素为一个无障碍元素，必须在UIAccessibilityAction协议中实现accessibilityIncrement 和accessibilityDecrement。Available in iOS 4.0 and later.
    UIAccessibilityTraitAllowsDirectInteraction ：无障碍元素允许voiceover用户直接触摸交互。可以使用这个元素描述无障碍元素，这个元素呈现一个用户可以直接交互的对象，比如一个呈现钢琴键盘的视图；Available in iOS 5.0 and later.
    UIAccessibilityTraitCausesPageTurn ：当voiceover读完当前页的文本时，这个无障碍元素应该引起自动翻页。可以使用这个元素来描述无障碍元素，这个元素呈现一系列网页中一页内容，比如一个呈现某页书的视图。当voiceover读完当前页，调用具有UIAccessibilityScrollDirectionNext的accessibilityScroll来滚动到下一页。如果voiceover检测到新内容与之前的内容相同，会停止滚动。Available in iOS 5.0 and later.
    UIAccessibilityTraitHeader ：这个无障碍元素是个将内容分段的标题，比如导航条标题。Available in iOS 6.0 and later.


    Notification Dictionary Keys
    被使用在通知中userInfo参数字典的键。
    声明：
    SWITF
    let UIAccessibilityAnnouncementKeyStringValue: String
    let UIAccessibilityAnnouncementKeyWasSuccessful: String
    OBJECTIVE-C
    NSString *const UIAccessibilityAnnouncementKeyStringValue;
    NSString *const UIAccessibilityAnnouncementKeyWasSuccessful;
    常量：
    UIAccessibilityAnnouncementKeyStringValue ：已完成通知的文本。Available in iOS 6.0 and later.
    UIAccessibilityAnnouncementKeyWasSuccessful ：指明通知是不是成功制作。这个键的值是个NSNumber对象，应该被翻译为布尔值。Available in iOS 6.0 and later.

    Speech Attributes for Attributed Strings
    可以应用于属性文本的属性，来修改文本是怎样发音的。
    声明：
    SWIFT
    let UIAccessibilitySpeechAttributePunctuation: String
    let UIAccessibilitySpeechAttributeLanguage: String
    let UIAccessibilitySpeechAttributePitch: String
    OBJECTIVE-C
    NSString *const UIAccessibilitySpeechAttributePunctuation;
    NSString *const UIAccessibilitySpeechAttributeLanguage;
    常量
    UIAccessibilitySpeechAttributePunctuation ：该键的值一个NSNumber对象，可以被翻译为布尔值。当值为YES时，文本中所有标点都会被读出。可以使用这个来读代码或者其他标点有关文本。Available in iOS 7.0 and later.
    UIAccessibilitySpeechAttributeLanguage ：这个键的值是一个NSString对象，包含BCP-47语言编码。当被应用到文本，指定语言规则会决定该文本是怎样发音的。Available in iOS 7.0 and later.
    UIAccessibilitySpeechAttributePitch ：这个键的值是一个NSNumber对象，包含一个浮点型值，从0.0到2.0.这个值指明文本是否应该使用比默认高或低的声调读出。这个属性的默认值是1.0，是个正常的音调。0.0-1.0的结果是一个低的声调，1.0-2.0的值是一个高的声调。Available in iOS 7.0 and later. 

    Assistive Technology Identifiers
    但当暂停恢复辅助技术时可以使用的标示符。
    声明：
    SWIFT
    let UIAccessibilityNotificationSwitchControlIdentifier: String
    OBJECTIVE-C
    NSString *const UIAccessibilityNotificationSwitchControlIdentifier;
    常量：
    UIAccessibilityNotificationSwitchControlIdentifier ：开关控制技术。这个技术允许行动不便的用户使用一个单一物理按键来访问app。当这个技术启动时，ios会在屏幕上圈一个光标，从一个元素到一个元素。用户点击开关来运行光标下的严肃。Available in iOS 8.0 and later.

    UIAccessibilityNavigationStyle
    一个常量，描述了辅助技术应该怎样导航对象元素。
    SWIFT
    enum UIAccessibilityNavigationStyle : Int {
        case Automatic
        case Separate
        case Combined
    }
    OBJECTIVE-C
    typedef enum UIAccessibilityNavigationStyle : NSInteger {
       UIAccessibilityNavigationStyleAutomatic = 0,
       UIAccessibilityNavigationStyleSeparate = 1,
       UIAccessibilityNavigationStyleCombined = 2,
    } UIAccessibilityNavigationStyle;
    常量：
    UIAccessibilityNavigationStyleAutomatic ：辅助技术会自动决定接收器元素怎样被导航，这个是默认值。Available in iOS 8.0 and later.
    UIAccessibilityNavigationStyleSeparate ：接收器元素应该被当做单独元素被导航。Available in iOS 8.0 and later.
    UIAccessibilityNavigationStyleCombined ：接收器元素应该组合并且被当做单独条目导航。Available in iOS 8.0 and later.

### 3.5通知


    UIAccessibilityAnnouncementNotification
    当一个通知需要被传递给辅助技术的时候，这个通知被应用推送。这个通知包含一个参数，是一个包含通知的NSString对象。辅助技术会输出这个参数里面的声明文本。使用这个通知提供事件的无障碍信息，这个事件不会刷新用户界面，或者只是文本的刷新。使用UIAccessibilityPostNotification功能传递这个通知。
    声明：
    SWIFT
    var UIAccessibilityAnnouncementNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityAnnouncementDidFinishNotification
    当系统讲完一个公告，UIKit推送该通知。参数是一个具有两个关键点的字典，UIAccessibilityAnnouncementKeyStringValue和UIAccessibilityAnnouncementKeyWasSuccessful。使用默认通知中心监听给通知。
    声明：
    SWIFT
    let UIAccessibilityAnnouncementDidFinishNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit


    UIAccessibilityBoldTextStatusDidChangeNotification
    当系统粗体文本发生变化时，由UIKit推送。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityBoldTextStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilityClosedCaptioningStatusDidChangeNotification
    当隐藏字幕（closed captioning）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityClosedCaptioningStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityDarkerSystemColorsStatusDidChangeNotification
    当系统的变暗颜色（Darken Colors）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityDarkerSystemColorsStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    
    UIAccessibilityGrayscaleStatusDidChangeNotification
    当系统的灰阶（Grayscale）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityGrayscaleStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityGuidedAccessStatusDidChangeNotification
    当系统的引导访问（Guided Access ）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。也可以使用
    UIAccessibilityIsGuidedAccessEnabled功能来判定当前的引导访问是不是可用的。
    声明：
    SWIFT
    let UIAccessibilityGuidedAccessStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityInvertColorsStatusDidChangeNotification
    当系统的反色（inverted colors）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。也可以使用
    UIAccessibilityIsInvertColorsEnabled功能来判定当前的引导访问是不是可用的。
    声明：
    SWIFT
    let UIAccessibilityInvertColorsStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityLayoutChangedNotification
    当系统的屏幕布局改变时，应用推送该通知，比如当一个元素出现或消失时。这个通知包含一个参数，这个参数是个voiceover讲出的NSSting对象或者可以接收焦点的无障碍元素。使用UIAccessibilityPostNotification功能推送该通知。
    声明：
    SWIFT
    var UIAccessibilityLayoutChangedNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityMonoAudioStatusDidChangeNotification
    当系统音频从立体声变为单声道时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityMonoAudioStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilityPageScrolledNotification
    当完成滚动操作且accessibilityScroll被调用时，应用推送该通知。这个通知包含一个参数，这个参数是一个NSString对象，包含新滚动位置的描述。辅助技术输入参数中的描述文本。在用户施行了voiceover滚动手势，可以使用该通知来提供屏幕内容的自定义信息。例如，一个基于tab的应用可能提供一个文本，如“tab 3 of 5”，或者在页面中展示信息的应用提供例如“Page 19 of 27”的文本。当辅助技术重复接收到相同滚动位置文本，这表明用户到达边或边界。使用UIAccessibilityPostNotification功能推送该通知。
    声明：
    SWIFT
    var UIAccessibilityPageScrolledNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityPauseAssistiveTechnologyNotification
    当想要暂时停止辅助技术的运行时推送该信息。当推送该通知，指定要暂停的辅助技术作为参数。例如，当app在播放动画的时候，想要在Switch Control中暂停扫描。相对的，通过推送UIAccessibilityResumeAssistiveTechnologyNotification通知恢复辅助技术的运行。使用UIAccessibilityPostNotification功能推送这个通知。
    声明：
    SWIFT
    var UIAccessibilityPauseAssistiveTechnologyNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilityReduceMotionStatusDidChangeNotification
    当系统的减少运动（reduce motion）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    使用UIAccessibilityPostNotification功能推送这个通知。
    声明：
    SWIFT
    let UIAccessibilityReduceMotionStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityReduceTransparencyStatusDidChangeNotification
    当系统的降低透明度（Reduce Transparency）的设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityReduceTransparencyStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilityResumeAssistiveTechnologyNotification
    推送此通知来暂时恢复辅助技术的运行。当推送此通知，指定辅助技术作为一个参数。必须推送此通知来平衡之前的UIAccessibilityPauseAssistiveTechnologyNotification推送通知。使用UIAccessibilityPostNotification功能来推送此通知。
    声明：
    SWIFT
    var UIAccessibilityResumeAssistiveTechnologyNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilityScreenChangedNotification
    当一个新的视图出现且占了屏幕的主要部分时，推送该通知。这个通知包含一个参数，是个NSString对象或者可以接收voiceover焦点的无障碍元素。使用UIAccessibilityPostNotification推送该通知。
    声明：
    SWIFT
    var UIAccessibilityScreenChangedNotification: UIAccessibilityNotifications
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

    UIAccessibilitySpeakScreenStatusDidChangeNotification
    当系统的读屏设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilitySpeakScreenStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilitySpeakSelectionStatusDidChangeNotification
    当系统的声音选择设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilitySpeakSelectionStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit


    UIAccessibilitySwitchControlStatusDidChangeNotification
    当系统的开关控件设置改变时，UIKit推送该通知。这个通知不包含参数。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilitySwitchControlStatusDidChangeNotification: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit
    
    UIAccessibilityVoiceOverStatusChanged
    当voiceover开启和停止时，推送该焦点。这个通知不包含参数。可以使用这个参数为voiceover用户自定义应用用户界面。例如，如果一个UI元素覆盖了UI的其他部分，可以为voiceover用户呈现一样的布局，但是允许非voiceover用户取消。可以使用UIAccessibilityIsVoiceOverRunning功能来判定voiceover是否在运行。使用默认通知中心监听这个通知。
    声明：
    SWIFT
    let UIAccessibilityVoiceOverStatusChanged: String
    导入声明：
    OBJECTIVE-C
    @import UIKit
    SWIFT
    import UIKit

## 4.UI无障碍元素类（UIAccessibilityElement）


    文档参考来源：https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityElement_Class/index.html#//apple_ref/occ/cl/UIAccessibilityElement
    UIAccessibilityElement类封装了应该对残障用户无障碍的条目信息，但是这些条目默认不是无障碍的。例如，一个图标或者文本图片不是自动无障碍的，因为它们不会继承UIView或者UIControl，一个包含非视图条目的视图需要创建了一个无障碍呈现的UIAccessibilityElement视图。
    一个无障碍元素的属性为辅助应用提供元素的信息，比如位置和当前的值。可能需要去设置元素的属性，即使不需要创建UIAccessibilityElement实例来呈现它。例如，如果应用包含一个含义为solve自定义图标按钮，按钮已经以无障碍元素呈现，因为它是UIButton的一个子类。但是，需要提供label或hint信息，因为这些信息对这个按钮来说是独一无二的。可以在 Interface Builder或者在UIAccessibility非正式协议中设置这些属性。

### 4.1创建一个无障碍元素


    - initWithAccessibilityContainer:
    创建并初始化一个无障碍元素，在一个指定容器中呈现条目。一般情况下，不需要在应用中为条目创建无障碍元素，因为标准UIKit控件和视图默认是无障碍的。但是如果视图包含一个非视图条某，比如图标和文本图像，需要对残障用户无障碍，需要为它们创建无障碍元素。在这个案例中，包含视图应该实现UIAccessibilityContainer非正式协议，并且使用这个方法去创建一个无障碍元素来呈现每一个条目，这些条目应该被辅助应用获得。
    声明：
    - (id)initWithAccessibilityContainer:(id)container
    参数：container——包含条目的视图。

### 4.2访问包含视图（Accessing the Containing View）


    accessibilityContainer：
    包含无障碍元素的视图。
    声明：
    @property(nonatomic, assign) id accessibilityContainer


### 4.3判定无障碍


    isAccessibilityElement：
    一个布尔值，指明该条目是不是一个无障碍应用可以访问的无障碍元素。这个属性的默认值是flase。如果接收器是个UIKit控件，默认值是true。
    声明：
    @property(nonatomic, assign) BOOL isAccessibilityElement

### 4.4访问无障碍元素的属性


    accessibilityLabel：
    属性，简洁指明无障碍元素的文本；label非常短，使用本地语言来指明无障碍元素，不包含控件和视图的类型。例如，一个保存按钮的label为Save，不是Save Button。默认的，标准UIKit控件和视图包含从title中派生出的label信息。如果提供自定义控件或者视图，需要适当的去设置这个属性，这样辅助应用可以提供给残障用户最精确的信息。
    声明：
    @property(nonatomic, retain) NSString *accessibilityLabel
    
    accessibilityHint：
    属性，简洁描述无障碍元素的操作结果；hint是个简短的本地化描述，描述的是一个无障碍元素操作的结果，而不是指明元素或者行为。例如，一个包含email信息的表行应该是“选择信息”。而不是“点击该行去选择信息”。默认的，标准UIKit控件和视图是系统提供hint。如果提供一个自定义控件和视图时，但是，需要适当去设置该属性，这样辅助应用可以为残障用户提供精确信息。
    声明：
    @property(nonatomic, retain) NSString *accessibilityHint

    accessibilityValue：
    属性，呈现无障碍元素的当前值文本；value值是个本地化文本，包含元素的当前值。例如，一个滑块的值可能是9.5或者35%，文本域的值是就是包含的文本。只有当一个无障碍元素有一个无法通过label呈现的值时，才能使用value属性。例如，一个音量滑块的label可能是“音量”，但是它的value值是当前音量级别。在这个案例中，用户不能很好的了解滑块的特性，因为用户也需要知道当前的值。保存按钮的label，告诉用户需要知道的关于控件的所有信息；提供“保存”作为value值会不必要且令人困扰。
    声明：
    @property(nonatomic, retain) NSString *accessibilityValue
    
    accessibilityFrame：
    属性，在屏幕坐标上无障碍元素的框架；当创建一个无障碍元素来呈现应用中的一个元素，必须设置这个属性到CGRect结构，这个结构指明对象的屏幕位置和大小。（继承自UIView的对象默认包含该信息）。
    声明：
    @property(nonatomic, assign) CGRect accessibilityFrame

    accessibilityTraits：
    属性，最能描述无障碍元素的特性组合。一个trait描述了一个元素行为、状态、使用中的一个方面。这个属性将几个trait组合，给辅助应用关于该元素一个全面的描述。可查看UIAccessibility Protocol Reference中“Accessibility Traits”的traits列表。
    UIKit为所有标准控件和视图，提供合适的trait组合。当为一个自定义无障碍元素组合特性时，要保证：
    使用常识。如果描述元素的特性是相互排斥的，不要组合特性，比如将按钮和搜索区域的特性组合。
    使用superclass特性组合已选择的特性。具体的说，使用[super accessibilityTraits]和用来设置自定义特性的方法组合自定义特性。
    声明：
    @property(nonatomic, assign) UIAccessibilityTraits accessibilityTraits

## 5.UI无障碍容器（UIAccessibilityContainer）


    文档参考来源：https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIAccessibilityContainer_Protocol/#//apple_ref/occ/instp/NSObject/accessibilityElements
    UIAccessibilityContainer非正式协议为UIView子类提供一个方式，将已选择的无障碍元素作为独立元素标记。例如，一个可能包含图标或者文本图片视图，对最终用户来说，出现和功能是作为一个独立条目的。但是因为这些元素不是作为UIView实例实现的，这些元素不会自动对残障用户无障碍。因此，此类容器视图应该实现UIAccessibilityContainer方法来提供这些元素的无障碍信息来帮助像voiceover这样的辅助应用。
    实现UIAccessibilityContainer非正式协议的视图使用UIAccessibilityElement方法initWithAccessibilityContainer：创建一个无障碍元素呈现每一个需要对残障用户无障碍的非视图元素。注意，但是，容器视图本身不是一个无障碍元素，因为用户不会与之交互。这一位置容器视图实现UIAccessibilityContainer必须将UIAccessibility 非正式协议的 isAccessibilityElement属性为NO。
    容器视图内无障碍元素的顺序应该与呈现给用户的顺序相同，从左到右，从上到下。

### 5.1提供有关无障碍元素的信息


    - accessibilityElementCount
    返回容器内无障碍元素的数量。默认为0。
    声明：
    SWIFT
    func accessibilityElementCount() -> Int
    OBJECTIVE-C
    - (NSInteger)accessibilityElementCount
    版本信息：Available in iOS 3.0 and later.
    
    - accessibilityElementAtIndex:
    按照特定索引返回无障碍信息，没有元素返回nil。
    声明：
    SWIFT
    func accessibilityElementAtIndex(_ index: Int) -> AnyObject?
    OBJECTIVE-C
    - (id _Nullable)accessibilityElementAtIndex:(NSInteger)index
    参数：index——无障碍元素的索引。
    版本：Available in iOS 3.0 and later.
    
    - indexOfAccessibilityElement:
    返回指定无障碍元素的索引，无元素返回NSNotFount。
    声明：
    SWIFT
    func indexOfAccessibilityElement(_ element: AnyObject) -> Int
    OBJECTIVE-C
    - (NSInteger)indexOfAccessibilityElement:(id _Nonnull)element
    参数：element——无障碍元素
    版本：Available in iOS 3.0 and later.

    accessibilityElements
    容器内无障碍元素的数组，默认值为nil。
    声明：
    SWIFT
    var accessibilityElements: [AnyObject]?
    OBJECTIVE-C
    @property(nonatomic, strong, nullable) NSArray *accessibilityElements
    版本：Available in iOS 8.0 and later.

## 6.UIGuidedAccessRestrictionDelegate


    文档参考来源：https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIGuidedAccessRestrictionsDelegate_Protocol/#//apple_ref/occ/intfm/UIGuidedAccessRestrictionDelegate/guidedAccessRestrictionIdentifiers

    在应用代理中使用UIGuidedAccessRestrictionDelegate协议允许在ios为Guided Access功能添加自定义限制。
    自定义限制在guidedAccessRestrictionIdentifiers方法中，通过开发者提供的文本标示符呈现。每一个标示符表示app中的一个操作，app希望允许用户限制使用Guided Access。所有操作的默认值是允许。用户可以使用正常Guided Access用户界面拒绝操作。详情见http://support.apple.com/kb/HT5509。
    App通过实现textForGuidedAccessRestrictionWithIdentifier:和detailTextForGuidedAccessRestrictionWithIdentifier: 方法来返回适当的本地的、可读的文本。
    例如，一个照片编辑app可能允许用户禁止删除照片。App将会在detailTextForGuidedAccessRestrictionWithIdentifier: 方法中返回一个标示符呈现这个限制。App也会实现textForGuidedAccessRestrictionWithIdentifier: 方法来提供一个可读的限制描述。最后，app将会实现guidedAccessRestrictionWithIdentifier:didChangeState:来通知，当用户表示希望激活这个限制的时候。当app看见状态变为拒绝，将会配置自己通说任何方式阻止照片删除。相似的，当app看见状态变为允许，将会配置自己允许照片删除。
    App可以使用UIGuidedAccessRestrictionStateForIdentifier函数来检查限制的状态。


### 6.1确定自定义引导访问限制



    - guidedAccessRestrictionIdentifiers      Required
    返回一个文本数组确定自定义限制，是一个NSString对象数组，每一个呈现一个自定义限制。如果想在app中提供自定义引导访问，代理必须实现这个方法，并且为每一个自定义引导访问，返回一个标识符文本数组。
    声明:
    SWIFT
    func guidedAccessRestrictionIdentifiers() -> [String]?
    OBJECTIVE-C
    - (NSArray<NSString *> * _Nullable)guidedAccessRestrictionIdentifiers
    版本：Available in iOS 7.0 and later.
    
    - textForGuidedAccessRestrictionWithIdentifier:    Required
    为提供标识符返回一个简洁的限制描述，一个本地的、可理解的简单文本。
    声明：
    SWIFT
    func textForGuidedAccessRestrictionWithIdentifier(_ restrictionIdentifier: String) -> String?
    OBJECTIVE-C
    - (NSString * _Nullable)textForGuidedAccessRestrictionWithIdentifier:(NSString * _Nonnull)restrictionIdentifier
    参数:
    restrictionIdentifier	  系统感兴趣的限制标识符；
    版本：Available in iOS 7.0 and later.
    
    - detailTextForGuidedAccessRestrictionWithIdentifier:
    为提供的标识符限制返回更多详细信息，一个本地化、可理解的附加信息。
    声明：
    SWIFT
    optional func detailTextForGuidedAccessRestrictionWithIdentifier(_ restrictionIdentifier: String) -> String?
    OBJECTIVE-C
    - (NSString * _Nullable)detailTextForGuidedAccessRestrictionWithIdentifier:(NSString * _Nonnull)restrictionIdentifier
    参数：restrictionIdentifier  系统感兴趣的限制标示符。
    版本：Available in iOS 7.0 and later.
 
###    6.2实现限制


    - guidedAccessRestrictionWithIdentifier:didChangeState:      Required
    App需要更改自己的行为去允许和拒绝操作，是特定限制每一次接收到信息时特定限制的。
    声明：
    SWIFT
    func guidedAccessRestrictionWithIdentifier(_ restrictionIdentifier: String,
                                didChangeState newRestrictionState: UIGuidedAccessRestrictionState)
    OBJECTIVE-C
    - (void)guidedAccessRestrictionWithIdentifier:(NSString * _Nonnull)restrictionIdentifier
                                   didChangeState:(UIGuidedAccessRestrictionState)newRestrictionState
    参数：
    restrictionIdentifier	——限制标示符，状态会改变。
    newRestrictionState——限制的新状态。
    版本：Available in iOS 7.0 and later.

### 6.3常量


    UIGuidedAccessRestrictionState
    限制的状态，允许或拒绝；
    声明：
    SWIFT
    enum UIGuidedAccessRestrictionState : Int {
        case Allow
        case Deny
    }
    OBJECTIVE-C
    typedef enum : NSInteger {
       UIGuidedAccessRestrictionStateAllow,
       UIGuidedAccessRestrictionStateDeny 
    } UIGuidedAccessRestrictionState;
    常量：
    UIGuidedAccessRestrictionStateAllow app  应该允许用户操作，这个操作是被限制控制的。Available in iOS 7.0 and later.
    UIGuidedAccessRestrictionStateDeny  应该拒绝用户操作，这个操作是被限制控制的。Available in iOS 7.0 and later.
    引入声明：
    OBJECTIVE-C
    @import UIKit;
    SWIFT
    import UIKit
    版本：Available in iOS 7.0 and later.
 


## 7.IOS默认无障碍属性信息


    作为标准UIKit控件和视图内置无障碍性的一部分，iOS已经提供了一些VoiceOver可以使用的默认的属性信息。大多数情况下这些信息已经足够了。然而，有时候你可以修改这些信息从而增强VoiceOver的用户体验：
    如果你使用一个标准UIKit控件或者视图来展示一个系统提供的图标或者标题，首先确认你的用法是否符合它们的含义（参见“iOS用户界面教程”），然后确认默认的标签属性是否能让用户理解这个控件或者视图的效果。如果不能的话，最好提供一个提示属性。
    举例来说，如果你想在导航栏中放置一个添加按钮并在UIBarButtonItem对象中使用系统提供的加（+）图标，那它会自动包含一个默认的标签属性：添加。如果用户可以明确地知道每次点击这个按钮会添加哪个项目，那就不需要提供提示属性。但是如果可能产生误解的话，你应该提供一个自定义的提示并描述使用这个按钮的效果，比如“添加一个账户”或者“添加一个评论”。
    如果你在标准的UIKit视图（比如UIButton对象）中展示一个自定义的图标或者图片，那你需要提供一个自定义标签属性来进行描述。
    用来描述无障碍用户界面元素的无障碍属性构成了UI Accessibility API的核心。当用户访问或操作控件和视图时，VoiceOver会告知用户无障碍属性的相关信息。
    因为无障碍属性封装了区分不同控件和视图的信息，所以无障碍属性也是你最有可能用到的编程接口的组件。就标准UIKit控件和视图来说，确保应用中默认的属性信息准确可能就够了。就自定义的控件和视图来说，或许要添加大部分的属性信息。
    UI Accessibility 编程接口定义了如下属性：
    标签label：一个简短的本地化词或短语，此短语简洁地描述控件或者视图，但是不能识别元素类型。例如“添加”、“播放”。
    特征traits：一个或多个独立特征的组合。每个特征描述一个元素状态、行为、使用中的某一方面。例如当元素的行为如同被选中键盘上的按键，这个元素就有了Keyboard Key和Selected的组合特征。
    提示hint：一个简短的本地化短语，描述发生在元素上动作的结果。例如“添加标题”或者“打开购物列表”。
    框架Frame：元素在屏幕上坐标的框架。由CGRect结构体提供，详细说明了元素的屏幕位置和大小。
    值value：不是由标签定义的元素时的当前值。例如，一个幻灯片的标签可以是”速度”，但是它当前的值是“50%”。
    

    图3 显示了VoiceOver可以提供了一些信息。
    VoiceOver用户靠听标签和提示来使用应用。因此，确保应用中的每一个无障碍元素提供准确全面的描述是极其重要的。标准UIKit控件和视图的默认值信息经常是准确的，但是你应该检查一下确保无误。对于自定义控件和视图，你可能不得不自己提供部分或者全部信息。关于如何去提供这些信息的指导，请看“打造好用的标签和提示”；

## 8.自定义视图--创建有用的标签和提示



### 8.1 label属性用来识别用户界面元素


    每一个无障碍用户界面元素、标准和自定义，必须支持label属性。
    有一个确定标签label内容的好办法，那就是思考一下正常的用户只通过视觉观察可以获得什么信息。如果你的用户界面设计得很好的话，正常的用户应该可以通过阅读标题和图标来了解控件和视图的作用。同理，VoiceOver用户需要从标签label属性中获取的就是这些信息。
    如果你使用的是自定义控件或者视图，或者在标准控件和视图中使用了自定义图标，那你需要提供包含下面内容的标签label：
    1)简洁的描述元素：如果标签label只包含一个词那就最好了，比如“添加”、“播放”、“删除”、“搜索”、“喜欢”和“音量”；
    2)好好设计你的应用，让每个元素的含义和用法在当前上下文中可以通过一个词来表示。然而，有时候可能必须要使用一句话才能准确描述一个元素。这时选择一个尽量短的句子，比如“播放音乐”、“添加姓名”或者“添加到事件中”；
    3)不要包含控件或者视图的类型。类型信息包含在元素的特性属性中，因不需要在标签中重复。举例来说，如果你的添加按钮包含控件类型，那VoiceOver用户听到的是“添加按钮按钮”。用户体验非常不好；
    4)不要用句号结束。标签并不是一句话因此并不需要用句号结束；
    5)支持本地化。

### 8.2 提示hint属性描述了控件和视图执行结果


    当label标签不能给出明确的目的描述时，应该提供hint属性来描述结果。
    举例来说，如果你的应用中有一个播放按钮，那用户可以根据上下文很清楚地判断出按下这个按钮有什么结果。然而，如果你允许用户通过点击列表中的歌名来播放歌曲，那你就需要创建一个提示来进行描述。原因是列表项目的标签label描述的是项目本身（在本例中是指歌名），并不是用户点击它的结果。
    如果label不能将控件和视图的执行结果描述清楚，应该创建一个hint：
    1)简介的描述结果。即使需要提示的控件和视图很少，还是要尽量让描述更简洁。这样可以减少用户在使用元素前需要花费在听上的时间。
    2)用动词开头并不使用祈使句。确保使用第三人称单数的动词形式，比如“Plays”，不要用祈使句“Play”，因为后者听起来像一条命令。比如说，你肯定不希望用户听到的是“播放这个歌曲”，而是“可以播放歌曲”。
    3)使用句号。即使提示只是一条短语，不是一句话，也要用句号结束。这可以帮助VoiceOver用合适的语气来朗读它。
    4)不要包含动作或者手势的名称。提示并不会告诉用户如何触发动作，它只告诉用户动作的结果。因此，不要创建类似“点击来播放音乐”、“点击来购买项目”或者“滑动来删除项目”这样的提示。
    5)不要包含控件或者视图的名字。用户可以从标签属性中获取这个信息，所以不需要在提示中重复。因此，不要创建类似“保存按钮可以保存你的编辑”或者“返回按钮会返回到之前的屏幕”这样的提示。
    6)不要包含控件或者视图的类型。用户可以通过元素的特性属性来获取这个信息，因此不要创建类似“用来添加姓名的按钮”或者“用来控制缩放的滑块”这样的提示。
    7)支持本地化。和无障碍标签一样，提示也需要进行本地化。

### 8.3选择合适的特性


    Traits属性包含一个或多个特性，组合起来，可以描述无障碍界面元素的行为。因为一些traits属性可以组合起来描述单独的元素，元素的行为可以准确描述。
    一个标准的UIKit控件，比如一个按钮或者文本框，都会在特性属性中提供默认的内容。如果你创建了一个自定义控件或者视图，那就必须提供元素特性属性的内容。
    UI无障碍编程接口定义了12个独立的特性，有些是可以组合的。有些特性描述的是控件类型（比如按钮）或者对象类型（比如图片）。有些特性描述的是控件的行为，比如可以播放引用。
    你可以在应用中使用下面的特性来描述元素：按钮、链接、搜索框、键盘按键、图片、播放音乐、选择、总觉元素、频繁更新、不可用、空；
    通常来说，控件类型特性可以和描述行为特性组合。举例来说，你可以组合“按钮”特性和“播放音乐”特性来描述一个自定义控件，它是一个按钮，点击的时候可以播放音乐。
    大多数情况下你可以认为控件类型特性是互斥的。也就是说，你不应该使用多余一个类型特性来描述应用中的元素，应该选择最合适的那个特性。然后，如果你的元素有额外的行为，可以用类型特性组合一个行为特性。
    举例来说，假设用户在iPhone的Safari中点击一个链接会显示一个图片，那你应该组合“图片”和“链接”特性来描述这个元素。另一个例子是点击键盘按键的时候会修改另一个键盘按键。你可以组合“键盘按键”和“选择”特性来描述这个元素。


## 9.修改用户界面无障碍属性


    iOS SDK 3.0自带一个Interface Builder，其中包含应用无障碍性相关的功能。如果你的应用包含标准UIKit控件和视图，那你可以在Interface Builder中完成所有的无障碍工作。
### 9.1在Interface Builder为标准控件和视图添加无障碍信息；
    可以使用Interface Builder设置元素的无障碍状态并提供自定义的标签、提示和特性属性的内容。具体的设置方法是，在你的nib文件中选择用户界面元素并打开Idendidy标签，可以在Accessibility部分看到下图的内容：
    
    图4  Interface Builder中所显示的标准文本框的默认无障碍信息。
    如图所示，nib文件中使用的标准的文本框默认是无障碍的，并且包含默认的标签、提示和特性属性的信息。（注意，对于包含占位符文字的文本框来说，默认标签是占位符文本。）你可以任意修改这些默认值，如下图所示（下图同样展示了Accessibility标签如何展示文本框的无障碍信息。具体的使用方法参见“在iOS模拟器中使用Accessibility Inspector调试无障碍性”）：
    
    图5 ios无障碍属性及属性查看

### 9.2让自定义独立视图支持无障碍使用


    如果你创建一个自定义视图来展示信息或者和用户进行交互，那你必须确保这些视图支持无障碍使用。无障碍化之后，你需要确认这些视图的确包含用户需要的无障碍信息。
    从无障碍的角度来说，自定义视图要不就是一个独立的视图，要不就是一个容器视图。独立视图并不包含其他需要支持无障碍的视图。举例来说，一个自定义的UIControl子类会展示一个图标并具有按钮的行为，但是除了按钮本身之外并不包含其他可以和用户进行交互的元素。
    容器视图恰好相反，包含其他可以和用户进行交互的元素。举例来说，一个自定义的UIView子类会绘制一个几何图形，这个图形就是一个不同于容器视图的可以和用户进行交互的元素。容器视图内的独立元素并不会自动支持无障碍使用（因为它们不是UIView的子类），也不会自动提供任何无障碍信息。
    除了使用Interface Builder，还可以通过两种编程方法让自定义独立视图支持无障碍使用。第一种方法是在初始化视图的时候设置它的无障碍状态。如下面的代码片段所示：
```
@implementation MyCustomViewController
- (id)init
{
_view = [[[MyCustomView alloc] initWithFrame:CGRectZero] autorelease];
[_view setIsAccessibilityElement:YES];
/* Set attributes here. */
}```
    另一种方法是实现UIAccessibility协议的isAccessibilityElement方法。如下面的代码片段所示：
```
@implementation MyCustomView
/* Implement attribute methods here. */
- (BOOL)isAccessibilityElement
{
return YES;
}```

### 9.3通过编程定义自定义属性信息


    如果你愿意，可以通过编程来提供自定义属性的信息。如果你没有使Interface Builder的话可能会选择这么做。
    就像“让自定义独立视图支持无障碍使用”中描述的一样，你可以在实例化视图的视图子类中设置无障碍信息。两种方法都可以用，但是如果你的视图会动态展示数据或者经常改变内容的话，那在子类中实现属性方法比在实例中实现更好。举例来说，如果你想显示时间的话，那应该在子类刷新数据的方法中实现无障碍性，因为如果只在实例化子类的时候设置属性，那更新数据之后就无法支持无障碍使用了。
    下面的代码片段是基于“让自定义独立视图支持无障碍使用”的方法写成的，包含一些属性特有的方法。如果你想在子类中实现无障碍方法，那可以参考下面的代码：
```
@implementation MyCustomView
- (BOOL)isAccessibilityElement
{
return YES;
}
- (NSString *)accessibilityLabel
{
return NSLocalizedString(@"MyCustomView.label", nil);
}
/* This custom view behaves like a button. */
- (UIAccessibilityTraits)accessibilityTraits
{
return UIAccessibilityTraitButton;
}
- (NSString *)accessibilityHint
{
return NSLocalizedString(@"MyCustomView.hint", nil);
}
@end```
    如果你想在实例化视图的代码中使用UIAccessbility协议中设置属性的方法的话，那可以参考下面的代码：
```
@implementation MyCustomViewController
- (id)init
{
_view = [[MyCustomView alloc] initWithFrame:CGRectZero];
[_view setIsAccessibilityElement:YES];
[_view setAccessibilityTraits:UIAccessibilityTraitButton];
[_view setAccessibilityLabel:NSLocalizedString(@"view.label", nil)];
[_view setAccessibilityHind:NSLocalizedString(@"view.hint", nil)];
}```

### 9.4让自定义容器视图支持无障碍使用


    如果你的应用中展示了一个自定义视图，其中包含其他可以进行用户交互的元素，那你需要实现每个元素的无障碍使用。与此同时，你必须让容器视图本身不支持无障碍使用，因为用户是和容器的内容交互，不是和容器本身交互。
    为了实现这一点，你自定义的容器视图需要实现UIAccessibilityContainer协议。这个协议会定义一些方法并把可以访问的元素放入一个数组中。
    下面的代码片段展示了一个自定义容器视图的部分实现。可以看到这个容器视图只会在调用UIAccessibilityContainer协议的方法时才会创建无障碍元素数组。所以，如果iPhone的无障碍并没有被激活，那就不会创建数组。
```
@implementation MultiFacetedView
- (NSArray *)accessibleElements
{
if ( _accessibleElements != nil )
{
return _accessibleElements;
}
_accessibleElements = [[NSMutableArray alloc] init];
/* Create an accessibility element to represent the first contained element and initialize it as a component of MultiFacetedView. */
UIAccessibilityElement *element1 = [[[UIAccessibilityElement alloc] initWithAccessibilityContainer:self] autorelease];
/* Set attributes of the first contained element here. */
[_accessibleElements addObject:element1];
/* Perform similar steps for the second contained element. */
UIAccessibilityElement *element2 = [[[UIAccessibilityElement alloc] initWithAccessibilityContainer:self] autorelease];
/* Set attributes of the second contained element here. */
[_accessibleElements addObject:element2];
return _accessibleElements;
}
/* The container itself is not accessible, so MultiFacetedView should return NO in isAccessiblityElement. */
- (BOOL)isAccessibilityElement
{
return NO;
}
/* The following methods are implementations of UIAccessibilityContainer protocol methods. */
- (NSInteger)accessibilityElementCount
{
return [[self accessibleElements] count];
}
- (id)accessibilityElementAtIndex:(NSInteger)index
{
return [[self accessibleElements] objectAtIndex:index];
}
- (NSInteger)indexOfAccessibilityElement:(id)element
{
return [[self accessibleElements] indexOfObject:element];
}
@end```

### 9.5让非文字数据支持无障碍阅读


    有时应用会显示一些不能自动支持无障碍方法的数据，比如一张图片，这时需要在无障碍标签中提供信息，这样VoiceOver用户就可以理解图片传达的内容。此外，如果你用图形提供信息，例如一个使用星星进行评价评级的系统，应该确保无障碍label传达了图片背后的意义。
    下面的代码展示的是一个自定义视图，它会用星星的数量来表示项目的评分。代码展示了如何根据星星数量返回一个合适的无障碍标签：
```
@implementation RatingView
/* Other subclass implementation code here. */
- (NSString *)accessibilityLabel
{
  /* _starCount is an instance variable that contains how many stars to draw. */
NSInteger starCount = _starCount;
 if ( starCount == 1 )
   {
      ratingString = NSLocalizedString(@"rating.singular.label", nil); // here, ratingString is "star"
   }
   else
   {
      ratingString = NSLocalizedString(@"rating.plural.label", nil); // here, ratingString is "stars"
   }
   return [NSString stringWithFormat:@"%d %@", starCount, ratingString];
}
@end```

### 9.6使动态元素无障碍


    如果用户界面元素会动态改变，那需要确保无障碍信息也会随着更新。如果应用的布局发生改变，需要发送通知，这样VoiceOver才能帮助用户切换到新布局。UI Accessibility编程接口提供了两种通知类型，你可以使用它们。（具体的教程参见“UIAccessbility协议参考”中的“通知”。）
    如果用户界面元素可以有不同的状态，那你需要在代码中返回所有状态对应的无障碍信息。由于这些改变在用户的动作发生后发生，所以最好把实现添加到子类中而不是实例化子类的代码中。
    下面的代码展示了如何处理动态状态的改变以及如何在屏幕布局发生改变的时候发送通知。代码中的UIView子类的行为类似一个自定义键盘按键。按键的无障碍标签会根据实例的内容进行改变，并且会根据shift键是否按下进行改变。按键也会根据实例内容和是否被选中返回不同的无障碍特性。注意，下面的代码假设会有许多方法查询键盘的状态：
```
@implementation BigKey
(NSString *)accessibilityLabel
{NSString *keyLabel = [_keyLabel accessibilityLabel];
if ( [self isLetterKey] )
{
if ( [self isShifted] )
{
return [keyLabel uppercaseString];
}
else
{
return [keyLabel lowercaseString];
}
}
else
{
return keyLabel;
}
}
(UIAccessibilityTraits)accessibilityTraits
{
UIAccessibilityTraits traits = [super accessibilityTraits] | UIAccessibilityTraitKeyboardKey;
/ If this is the shift key and it's selected, users need to know that shift is currently in effect. /
if ( [self isShiftKey] && [self isSelected] )
{
traits |= UIAccessibilityTraitSelected;
}
return traits;
}
(void)keyboardChangedToNumbers
{
/ Code to perform the change to a number keyboard here. /
/ Send a notification of this change to the screen layout. /
UIAccessibilityPostNotification(UIAccessibilityLayoutChangedNotification, nil);
}
@end```

### 9.7让表格视图支持无障碍使用


    如果你的应用中展示了一个表格，它的每个单元格中包含非文字（或者不只是文字）的内容，那你可以通过一些方法让它更好地支持无障碍使用。同理，如果你的表格视图中每行展示的信息许多，那可以把这些信息聚合到标签中。
    如果应用中的单元格包含多种不同元素，首先要判断用户是直接和单元格进行交互还是和单个元素进行交互。如果用户需要访问单元格中的独立元素，那你应该：
    让每个独立元素都支持无障碍使用
    让单元格本身不支持无障碍使用
    在单元格的标签属性中简单描述单元格的所有内容。注意，在这种情况下标签也被看作是单元格中一个支持无障碍访问的元素。
    你可能已经发现了，包含多个项目（比如文字和控件）的单元格和容器视图很像。但是，你不需要把单元格看作是一个容器视图并实现任何UIAccessibilityContainer协议的方法，因为单元格本身就是一个容器。
    如果单元格包含许多块信息，那应该把这些信息都组合到一个标签属性中，这样VoiceOver用户可以用一个手势获取所有信息。
    一个很好的例子就是内置的股票应用。它并没有用单独的字符串来提供公司名、当前股票价格和价格波动，而是组合到一个标签中，听起来类似“苹果公司，432.39美元，涨幅1.3%”。注意标签中的逗号，当你结合多个片段的时候，可以使用逗号，这样VoiceOver就会在每个逗号短暂停留，让用户更容易理解信息。
    下面这段代码把两个元素的信息组合到一个标签中：
```
@implementation CurrentWeather
/* This is a view that provides weather information. It contains a city subview and a temperature subview, each of which provides a separate label. */
- (NSString *)accessibilityLabel
{
NSString *weatherCityLabel = [self.weatherCity accessibilityLabel];
NSString *weatherTempLabel = [self.weatherTemp accessibilityLabel];
/* Combine the city and temperature information so that VoiceOver users can get the weather information with one gesture. */
return [NSString stringWithFormat:@"%@, %@", weatherCityLabel, weatherTempLabel];
}```
@end

## 10.视图控件角度的无障碍


    处理管理视图控件的行为，一个视图控制器可以帮助控制app的无障碍性。一个无障碍app是一个可以被所有人使用的app，无论是残疾还是身体功能障碍，同时作为一个有用的工具保留其的功能性和易用性。
    为了保证无障碍性，一个ios app必须向Voiceover提供用户界面元素的信息。Voiceover，是一个屏幕阅读技术，被设计用来帮助视障群体，大声读出文本、图片和屏幕上的UI控件，这样视障用户就可以与这些元素进行交互。UIKit对象默认是无障碍的，但是在视图角度仍有事可做来解决无障碍问题。在一个较高的水平，这意味着应该保证：
    每一个用户可以交互的用户界面元素是无障碍的。这包括仅提供信息的元素，如静态文本和执行操作的控件。
    所有的无障碍元素提供准确和有用的信息。
    除了这些基本因素，一个视图控件voiceover的用户体验，可以通过编程式的设置voiceover焦点框、响应voiceover手势、观察无障碍通知等，来提升。

### 10.1移动voice光标到一个特定的元素


    当屏幕布局改变时，voiceover焦点框，也被称为voiceover光标，会被重置在屏幕表单的从左到右，从上倒下第一个元素上。当视图在屏幕上呈现时，可能需要改变第一个被聚焦的元素。
    例如，当导航控制器将一个视图控制器置到一个导航对战，voiceover光标落在导航条的返回按钮上。基于app，将焦点转移到导航条的标题或其他元素上，将会更有意义。
    要做到这一点，使用UIAccessibilityScreenChangedNotification和想要聚焦的元素调用 UIAccessibilityPostNotification，如以下样例所示：
    
    发布一个无障碍通知可以改变第一个朗读的元素：
```
@implementation MyViewController
- (void)viewDidAppear:(BOOL)animated
{
[super viewDidAppear:animated];
UIAccessibilityPostNotification(UIAccessibilityScreenChangedNotification,
self.myFirstElement);
}
@end```

    如果只是布局改变，而不是屏幕内容改变，比如从人像模式转换到风景模式，使用UIAccessibilityLayoutChangedNotification而不是使用UIAccessibilityScreenChangedNotification。
    注意：设备旋转引起的布局改变，需要重置voiceover光标的位置。

### 10.2响应特殊voiceover手势


    Voiceover用户可以使用特殊手势触发自定义操作。这些手势之所以特殊是因为被允许去定义这些手势的行为，不同于voiceover标准手势。可以在事件和视图控制器中覆盖一定的方法来检测这些特殊手势。
    手势应该首先检查有voiceover焦点命令的视图，然后继续响应链直到手势找到相应voiceover手势方法的实现。如果没有找到实现方法，系统默认的该手势的响应就会被触发。例如，如果在当前视图找到Magic Tap的实现，Magic Tap手势在音乐app中播放和暂停音乐。
    尽管可以提供想要的自定义逻辑，voiceover用户希望这些特殊手势的行为遵循一定的原则。像任何手势，一个voiceover手势的实现应该遵循一个模式，这样与无障碍app的交互保持直观。
    有4种特殊voiceover手势：
    Escape：两指Z型手势，关闭模态对话框，或者在导航层次上返回上一级。
    Magic tap：两指双击手势，执行最预期的操作。
    Three-Finger Scroll：三指清扫，垂直或水平滚动内容。
    Increment and Decrement：一指上下扫动，增加或减去具有调节属性的给定值。具有可调节无障碍特性的元素必须具备这些方法。
    注：所有特殊voiceover手势方法都会返回一个布尔值，决定是否通过响应链传输。要停止传输，返回YES，否则，返回NO。
    Escape
    如果当前视图覆盖底层内容——比如模态对话框或者警号——应该使用accessibilityPerformEscape方法来退出浮层。Escape手势就像一个键盘上的Esc键；可以退出当前的对话框，或者回到主内容。
    另一个使用案例是使用Escape手势回到上一层级导航页面。UINavigationController默认实现这个功能。如果设计了自定义的导航控件，应该设置Escape手势来返回上一级的导航，因为这是用户期望的功能。
    Magic Tap
    Magic Tap手势的目的是快速开启一个经常用到或者最期望的操作。例如，在苹果手机，这个手势用来拨打和乖挂断电话。在时钟app中，它用来开始和暂停秒表。如果你想要使用一个动作触发特定的操作，不管视图是否有voiceover的光标，应该在视图控制器中实现accessibilityPerformMagicTap方法。
    注意：如果想要Magic Tap手势在app的任何位置都执行相同的动作，在app delegate中实现accessibilityPerformMagicTap更加合适。
    Three-Finger Scroll
    accessibilityScroll：当voiceover用户执行三指滚动时触发方法。accessibilityScroll接收UIAccessibilityScrollDirection参数，这个参数可以决定滚动方向。如果有一个自定义滚动视图，在该视图上实现更合适。
    Increment and Decrement
    accessibilityIncrement和 accessibilityDecrement方法对可调节特性元素是必须的，应该在该视图自己实现。

### 10.3监听无障碍通知


    需要监听无障碍通知来触发回调方法。在特定情境下，UIKit触发无障碍通知。App可以通过监听无障碍通知来扩展无障碍功能。
    例如，如果监听到UIAccessibilityAnnouncementDidFinishNotification通知，可以触发一个方法来跟进voiceover讲话的完成。Apple在iBooks app实现这个方法。当Voiceover读完一本书的一行，iBooks 开启一个通知触发读出下一行的内容。如果是一页上的最后一行，回调的逻辑告知iBooks去翻译，在最后一行完成时继续于都。这允许逐行阅读导航文本，提供一个无缝的、不间断的阅读体验。
    使用默认通知中心，注册无障碍通知观察器。然后创建一个相同名字的方法来提供选择参数，如下例所示：
    无障碍通知观察期注册：
```
@implementation MyViewController
- (void)viewDidLoad
{
[super viewDidLoad];
[[NSNotificationCenter defaultCenter]
addObserver:self
selector:@selector(didFinishAnnouncement:)
name:UIAccessibilityAnnouncementDidFinishNotification
object:nil];
}
- (void)didFinishAnnouncement:(NSNotification *)dict
{
NSString *valueSpoken = [[dict userInfo]
objectForKey:UIAccessibilityAnnouncementKeyStringValue];
NSString *wasSuccessful = [[dict userInfo]
objectForKey:UIAccessibilityAnnouncementKeyWasSuccessful];
// ...
}
@end```

    UIAccessibilityAnnouncementDidFinishNotification将一个 NSNotification 字典作为一个参数，这个参数可以判定有效的讲话，并且讲话是否不间断的完成。如果Voiceover用户执行了暂停讲话手势或者滑到其他元素时，讲话在完成之前就会被终端。
    另一个需要提交的有用的通知是UIAccessibilityVoiceOverStatusChanged。它可以检测到voiceover的开关。如果voiceover在app之外的翻转，当app回到前台时会收到服务。因为UIAccessibilityVoiceOverStatusChanged不期待任何参数，在选择器中的方法不需要提阿南爱一个尾随冒号（：）。
    可以参考的全部可能通知的列表，可以参见UIAccessibility Protocol Reference的通知。记住，只可以查看被UIKit发表的通知，这些通知是NSString对象，不是app发表的int类型的通知。