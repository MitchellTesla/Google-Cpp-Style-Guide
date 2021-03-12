# Google-C-Style-Guide 2021
a comprehensive Google C++ Style Guide

 
Table of Contents
C++ Version

Header Files
Self-contained HeadersThe #define GuardInclude What You UseForward DeclarationsInline FunctionsNames and Order of Includes

Scoping
NamespacesInternal LinkageNonmember, Static Member, and Global FunctionsLocal VariablesStatic and Global Variablesthread_local Variables

Classes
Doing Work in ConstructorsImplicit ConversionsCopyable and Movable TypesStructs vs. ClassesStructs vs. Pairs and TuplesInheritanceOperator OverloadingAccess ControlDeclaration Order

Functions
Inputs and OutputsWrite Short FunctionsFunction OverloadingDefault ArgumentsTrailing Return Type Syntax

Google-Specific Magic
Ownership and Smart Pointerscpplint

Other C++ Features
Rvalue ReferencesFriendsExceptionsnoexceptRun-Time Type Information (RTTI)CastingStreamsPreincrement and PredecrementUse of constUse of constexprInteger Types64-bit PortabilityPreprocessor Macros0 and nullptr/NULLsizeofType Deduction (including auto)Class Template Argument DeductionDesignated InitializersLambda ExpressionsTemplate MetaprogrammingBooststd::hashOther C++ FeaturesNonstandard ExtensionsAliases

Inclusive Language

Naming
General Naming RulesFile NamesType NamesVariable NamesConstant NamesFunction NamesNamespace NamesEnumerator NamesMacro NamesExceptions to Naming Rules

Comments
Comment StyleFile CommentsClass CommentsFunction CommentsVariable CommentsImplementation CommentsPunctuation, Spelling, and GrammarTODO Comments

Formatting
Line LengthNon-ASCII CharactersSpaces vs. TabsFunction Declarations and DefinitionsLambda ExpressionsFloating-point LiteralsFunction CallsBraced Initializer List FormatConditionalsLoops and Switch StatementsPointer and Reference ExpressionsBoolean ExpressionsReturn ValuesVariable and Array InitializationPreprocessor DirectivesClass FormatConstructor Initializer ListsNamespace FormattingHorizontal WhitespaceVertical Whitespace

Exceptions to the Rules
Existing Non-conformant CodeWindows Code

Goals of the Style Guide

Why do we have this document?

There are a few core goals that we believe this guide should serve. These are the fundamental whys that underlie all of the individual rules. By bringing these ideas to the fore, we hope to ground discussions and make it clearer to our broader community why the rules are in place and why particular decisions have been made. If you understand what goals each rule is serving, it should be clearer to everyone when a rule may be waived (some can be), and what sort of argument or alternative would be necessary to change a rule in the guide.

The goals of the style guide as we currently see them are as follows:

Style rules should pull their weight
The benefit of a style rule must be large enough to justify asking all of our engineers to remember it. The benefit is measured relative to the codebase we would get without the rule, so a rule against a very harmful practice may still have a small benefit if people are unlikely to do it anyway. This principle mostly explains the rules we don’t have, rather than the rules we do: for example, goto contravenes many of the following principles, but is already vanishingly rare, so the Style Guide doesn’t discuss it.
Optimize for the reader, not the writer
Our codebase (and most individual components submitted to it) is expected to continue for quite some time. As a result, more time will be spent reading most of our code than writing it. We explicitly choose to optimize for the experience of our average software engineer reading, maintaining, and debugging code in our codebase rather than ease when writing said code. "Leave a trace for the reader" is a particularly common sub-point of this principle: When something surprising or unusual is happening in a snippet of code (for example, transfer of pointer ownership), leaving textual hints for the reader at the point of use is valuable (std::unique_ptr demonstrates the ownership transfer unambiguously at the call site).
Be consistent with existing code
Using one style consistently through our codebase lets us focus on other (more important) issues. Consistency also allows for automation: tools that format your code or adjust your #includes only work properly when your code is consistent with the expectations of the tooling. In many cases, rules that are attributed to "Be Consistent" boil down to "Just pick one and stop worrying about it"; the potential value of allowing flexibility on these points is outweighed by the cost of having people argue over them.
Be consistent with the broader C++ community when appropriate
Consistency with the way other organizations use C++ has value for the same reasons as consistency within our code base. If a feature in the C++ standard solves a problem, or if some idiom is widely known and accepted, that's an argument for using it. However, sometimes standard features and idioms are flawed, or were just designed without our codebase's needs in mind. In those cases (as described below) it's appropriate to constrain or ban standard features. In some cases we prefer a homegrown or third-party library over a library defined in the C++ Standard, either out of perceived superiority or insufficient value to transition the codebase to the standard interface.
Avoid surprising or dangerous constructs
C++ has features that are more surprising or dangerous than one might think at a glance. Some style guide restrictions are in place to prevent falling into these pitfalls. There is a high bar for style guide waivers on such restrictions, because waiving such rules often directly risks compromising program correctness.
Avoid constructs that our average C++ programmer would find tricky or hard to maintain
C++ has features that may not be generally appropriate because of the complexity they introduce to the code. In widely used code, it may be more acceptable to use trickier language constructs, because any benefits of more complex implementation are multiplied widely by usage, and the cost in understanding the complexity does not need to be paid again when working with new portions of the codebase. When in doubt, waivers to rules of this type can be sought by asking your project leads. This is specifically important for our codebase because code ownership and team membership changes over time: even if everyone that works with some piece of code currently understands it, such understanding is not guaranteed to hold a few years from now.
Be mindful of our scale
With a codebase of 100+ million lines and thousands of engineers, some mistakes and simplifications for one engineer can become costly for many. For instance it's particularly important to avoid polluting the global namespace: name collisions across a codebase of hundreds of millions of lines are difficult to work with and hard to avoid if everyone puts things into the global namespace.
Concede to optimization when necessary
Performance optimizations can sometimes be necessary and appropriate, even when they conflict with the other principles of this document.
The intent of this document is to provide maximal guidance with reasonable restriction. As always, common sense and good taste should prevail. By this we specifically refer to the established conventions of the entire Google C++ community, not just your personal preferences or those of your team. Be skeptical about and reluctant to use clever or unusual constructs: the absence of a prohibition is not the same as a license to proceed. Use your judgment, and if you are unsure, please don't hesitate to ask your project leads to get additional input.


Parting Thoughts:
Use common sense and BE CONSISTENT.

If you are editing code, take a few minutes to look at the code around you and determine its style. If they use spaces around their if clauses, you should, too. If their comments have little boxes of stars around them, make your comments have little boxes of stars around them too.

The point of having style guidelines is to have a common vocabulary of coding so people can concentrate on what you are saying, rather than on how you are saying it. We present global style rules here so people know the vocabulary. But local style is also important. If code you add to a file looks drastically different from the existing code around it, the discontinuity throws readers out of their rhythm when they go to read it. Try to avoid this.

OK, enough writing about writing code; the code itself is much more interesting. Have fun! 
 Justin Mitchell ©️ 2021
