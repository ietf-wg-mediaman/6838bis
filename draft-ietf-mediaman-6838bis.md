---
title: Media Type Specifications and Registration Procedures
abbrev: Media Type Registration
docname: draft-ietf-mediaman-6838bis-latest
date:
category: bcp
obsoletes: 6838

ipr: trust200902
keyword: Internet-Draft

stand_alone: yes
smart_quotes: no
pi: [toc, tocindent, sortrefs, symrefs, strict, compact, comments, inline]

venue:
  home: "https://datatracker.ietf.org/wg/mediaman/about/"
  repo: "https://github.com/ietf-wg-mediaman/6838bis/"

github-issue-label: 6838bis

author:
 -
    ins: M. Nottingham
    name: Mark Nottingham
    organization: Cloudflare
    postal:
      - Prahran
    country: Australia
    email: mnot@mnot.net
    uri: https://www.mnot.net/
 -
    ins: P. Resnick
    name: Pete Resnick
    organization:
    email: resnick@episteme.net

informative:
  MacOSUTIs:
    title: "Framework: Uniform Type Identifiers"
    target: https://developer.apple.com/documentation/uniformtypeidentifiers
    author:
     -
       org: Apple Computer, Inc.
    date: March 2024

  windowsClipboardNames:
    title: "Clipboard Formats"
    target: https://learn.microsoft.com/en-us/windows/win32/dataxchg/clipboard-formats
    author:
     -
       org: MicroSoft Inc.
    date: August 2020

--- abstract

This document defines procedures for the specification and registration of media types for use in HTTP, MIME, and other Internet protocols.

--- middle

# Introduction

Recent Internet protocols have been carefully designed to be easily extensible in certain areas. In particular, many protocols, including but not limited to HTTP {{?RFC2616}} and MIME {{!RFC2045}}, are capable of carrying arbitrary labeled content.

The mechanism used to label such content is a media type, consisting of a top-level type and a subtype, which is further structured into trees. Optionally, media types can define companion data, known as parameters.

A registration process is needed for these labels, so that the set of such values are defined in a reasonably orderly, well-specified, and public manner.

This document specifies the criteria for media type registrations and defines the procedures to be used to register media types ({{procedures}}) as well as media type structured suffixes ({{suffix-procedures}}) in the Internet Assigned Numbers Authority (IANA) central registry.

The location of the media type registry managed by these procedures is:

> http://www.iana.org/assignments/media-types/

## Historical Note

The media type registration process was initially defined for registering media types for use in the context of the asynchronous Internet mail environment. In this mail environment, there is a need to limit the number of possible media types, to increase the likelihood of interoperability when the capabilities of the remote mail system are not known. As media types are used in new environments in which the proliferation of media types is not a hindrance to interoperability, the original procedure proved excessively restrictive and had to be generalized. This was initially done in {{?RFC2048}}, but the procedure defined there was still part of the MIME document set. The media type specification and registration procedure is now a separate document, to make it clear that it is independent of MIME.

It may be desirable to restrict the use of media types to specific environments or to prohibit their use in other environments. This specification incorporates such restrictions into media type registrations in a systematic way. See {{non-requirements}} for additional discussion.

## Conventions Used in This Document

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in {{!RFC2119}} when they appear in ALL CAPS. They may also appear in lower or mixed case as plain English words, without any normative meaning.

This specification makes use of the Augmented Backus-Naur Form (ABNF) {{!RFC5234}} notation, including the core rules defined in Appendix B of that document.

# Media Type Registration Preliminaries

Registration of a new media type or types starts with the construction of a registration proposal. Registration may occur within several different registration trees that have different requirements, as discussed below. In general, a new registration proposal is circulated and reviewed in a fashion appropriate to the tree involved. The media type is then registered if the proposal is acceptable. The following sections describe the requirements and procedures used for each of the different registration trees.

# Registration Trees and Subtype Names

In order to increase the efficiency and flexibility of the registration process, different structures of subtype names can be registered to accommodate the different natural requirements for, e.g., a subtype that will be recommended for wide support and implementation by the Internet community, or a subtype that is used to move files associated with proprietary software. The following subsections define registration "trees" that are distinguished by the use of faceted names, e.g., subtype names that begin with a "tree." prefix. Note that some media types defined prior to this document do not conform to the naming conventions described below. See {{grandfather}} for a discussion of them.

## Standards Tree

The standards tree is intended for types of general interest to the Internet community. Registrations in the standards tree MUST be either:

1. in the case of registrations associated with IETF specifications, approved directly by the IESG, or

2. registered by a recognized standards-related organization using the "Specification Required" IANA registration policy {{!RFC5226}} (which implies Expert Review), or

3. approved by the Designated Expert(s) as identifying a "community format", as described in {{community}}.

The first procedure is used for registrations from IETF Consensus documents, or in rare cases when registering a grandfathered (see {{grandfather}}) and/or otherwise incomplete registration is in the interest of the Internet community. The registration proposal MUST be published as an RFC. When the registration RFC is in the IETF stream, it must have IETF Consensus, which can be attained with a status of Standards Track, BCP, Informational, or Experimental. Registrations published in non-IETF RFC streams are also allowed and require IESG approval. A registration can be either in a stand-alone "registration only" RFC or incorporated into a more general specification of some sort.

In the second case, the IESG makes a one-time decision on whether the registration submitter represents a recognized standards-related organization; after that, a Media Types Reviewer (Designated Expert or a group of Designated Experts) performs the Expert Review as specified in this document. Subsequent submissions from the same source do not involve the IESG. The format MUST be described by a formal standards specification produced by the submitting standards-related organization.

The third case is described in {{community}}.

Media types in the standards tree MUST NOT have faceted names, unless they are grandfathered in using the process described in {{grandfather}}.

The "owner" of a media type registered in the standards tree is assumed to be the standards-related organization itself. Modification or alteration of the specification uses the same level of processing (e.g., a registration submitted on Standards Track can be revised in another Standards Track RFC, but cannot be revised in an Informational RFC) required for the initial registration.

Standards-tree registrations from recognized standards-related organizations are submitted directly to the IANA, where they will undergo Expert Review {{!RFC5226}} prior to approval. In this case, the Expert Reviewer(s) will, among other things, ensure that the required specification provides adequate documentation.

## Community Formats in the Standards Tree {#community}

Some formats are interoperable (i.e., they are supported by more than one implementation), but their specifications are not published by a recognized standards-related organization. To accommodate these cases, the Designated Expert(s) are empowered to approve registrations in the standards tree that meet the following criteria:

- There is a well-defined specification for the format
- That specification is not tied to or heavily associated with one implementation
- The specification is freely available at a stable location
- There are multiple interoperable implementations of the specification, or they are likely to emerge
- The requested name is appropriate to the use case, and not so generic that it may be considered 'squatting'
- There is no conflict with IETF work or work at other recognised SDOs (present or future)
- There is evidence of broad adoption

The Designated Expert(s) have discretion in applying these criteria; in rare cases, they might judge it best to register an entry that fails one or more.

Note that such registrations still go through preliminary community review (Section 5.1), and decisions can be appealed (Section 5.3).

## Vendor Tree

The vendor tree is used for media types associated with publicly available products. "Vendor" and "producer" are construed very broadly in this context and are considered equivalent. Note that industry consortia as well as non-commercial entities that do not qualify as recognized standards-related organizations can quite appropriately register media types in the vendor tree.

A registration may be placed in the vendor tree by anyone who needs to interchange files associated with some product or set of products. However, the registration properly belongs to the vendor or organization producing the software that employs the type being registered, and that vendor or organization can at any time elect to assert ownership of a registration done by a third party in order to correct or update it. See {{change}} for additional information.

When a third party registers a type on behalf of someone else, both entities SHOULD be noted in the Change Controller field in the registration. One possible format for this would be "Foo, on behalf of Bar".

Vendor-tree registrations will be distinguished by the leading facet "vnd.". That may be followed, at the discretion of the registrant, by either a media subtype name from a well-known producer (e.g., "vnd.mudpie") or by an IANA-approved designation of the producer's name that is followed by a media type or product designation (e.g., vnd.bigcompany.funnypictures).

While public exposure and review of media types to be registered in the vendor tree are not required, using the media-types@iana.org mailing list for review is encouraged, to improve the quality of those specifications. Registrations in the vendor tree may be submitted directly to the IANA, where they will undergo Expert Review {{!RFC5226}} prior to approval.

## Personal or Vanity Tree

Registrations for media types created experimentally or as part of products that are not distributed commercially may be registered in the personal or vanity tree. The registrations are distinguished by the leading facet "prs.".

The owner of "personal" registrations and associated specifications is the person or entity making the registration, or one to whom responsibility has been transferred as described below.

While public exposure and review of media types to be registered in the personal tree are not required, using the media-types@iana.org mailing list (see {{preliminary-review}}) for review is encouraged, to improve the quality of those specifications. Registrations in the personal tree may be submitted directly to the IANA, where they will undergo Expert Review {{!RFC5226}} prior to approval.

## Unregistered x. Tree

Subtype names with "x." as the first facet may be used for types intended exclusively for use in private, local environments. Types in this tree cannot be registered and are intended for use only with the active agreement of the parties exchanging them.

However, with the simplified registration procedures described above for vendor and personal trees, it should rarely, if ever, be necessary to use unregistered types. Therefore, use of types in the "x." tree is strongly discouraged.

Note that types with names beginning with "x-" are no longer considered to be members of this tree (see {{?RFC6648}}). Also note that if a generally useful and widely deployed type incorrectly ends up with an "x-" name prefix, it MAY be registered using its current name in an alternative tree by following the procedure defined in {{grandfather}}.

## Additional Registration Trees

From time to time and as required by the community, new top-level registration trees may be created by IETF Standards Action. It is explicitly assumed that these trees may be created for external registration and management by well-known permanent organizations; for example, scientific societies may register media types specific to the sciences they cover. In general, the quality of review of specifications for one of these additional registration trees is expected to be equivalent to registrations in the standards tree by a recognized standards-related organization. When the IETF performs such review, it needs to consider the greater expertise of the requesting organization with respect to the subject media type.

# Registration Requirements

Media type registrations are all expected to conform to various requirements laid out in the following sections. Note that requirement specifics sometimes vary depending on the registration tree, again as detailed in the following sections.

## Functionality Requirement

Media types MUST function as actual media formats. Registration of things that are better thought of as a transfer encoding, as a charset, or as a collection of separate entities of another type, is not allowed. For example, although applications exist to decode the base64 transfer encoding {{!RFC2045}}, base64 cannot be registered as a media type.

This requirement applies regardless of the registration tree involved.

## Naming Requirements

All registered media types MUST be assigned top-level type and subtype names. The combination of these names serves to uniquely identify the media type, and the subtype name facet (or the absence of one) identifies the registration tree. Both top-level type and subtype names are case-insensitive.

Type and subtype names MUST conform to the following ABNF:

~~~ abnf
  type-name = restricted-name
  subtype-name = restricted-name

  restricted-name = restricted-name-first *126restricted-name-chars
  restricted-name-first  = ALPHA / DIGIT
  restricted-name-chars  = ALPHA / DIGIT / "!" / "#" /
                           "$" / "&" / "-" / "^" / "_"
  restricted-name-chars =/ "." ; Characters before first dot always
                               ; specify a facet name
  restricted-name-chars =/ "+" ; Characters after last plus always
                               ; specify a structured syntax suffix
~~~

Note that this syntax is somewhat more restrictive than what is allowed by the ABNF in {{Section 5.1 of !RFC2045}} or {{Section 4.2 of ?RFC4288}}. Also note that while this syntax allows names of up to 127 characters, implementation limits may make such long names problematic. For this reason, 'type-name' and 'subtype-name' SHOULD be limited to 64 characters.

Although the name syntax treats "." as equivalent to any other character, characters before any initial "." always specify the registration facet. Note that this means that facet-less standards- tree registrations cannot use periods in the subtype name.

Similarly, the final "+" in a subtype name introduces a structured syntax specifier suffix. Structured syntax suffix requirements are specified in {{suffixes}}.

While it is possible for a given media type to be assigned additional names, the use of different names to identify the same media type is discouraged.

These requirements apply regardless of the registration tree involved.

The choice of top-level type MUST take into account the nature of media type involved. New subtypes of top-level types MUST conform to the restrictions of the top-level type, if any. The following sections describe each of the initial set of top-level types and their associated restrictions. Additionally, various protocols, including but not limited to HTTP and MIME, MAY impose additional restrictions on the media types they can transport. (See {{!RFC2046}} for additional information on the restrictions MIME imposes.)

### Text Media Types

The "text" top-level type is intended for sending material that is principally textual in form.

Many subtypes of text, notably including the subtype "text/plain", which is a generic subtype for plain text defined in {{!RFC2046}}, define a "charset" parameter. If a "charset" parameter is defined for a particular subtype of text, it MUST be used to specify a charset name defined in accordance to the procedures laid out in {{!RFC2978}}.

As specified in {{!RFC6657}}, a "charset" parameter SHOULD NOT be specified when charset information is transported inside the payload (e.g., as in "text/xml").

If a "charset" parameter is specified, it SHOULD be a required parameter, eliminating the options of specifying a default value. If there is a strong reason for the parameter to be optional despite this advice, each subtype MAY specify its own default value, or alternatively, it MAY specify that there is no default value. Finally, the "UTF-8" charset {{!RFC3629}} SHOULD be selected as the default. See {{!RFC6657}} for additional information on the use of "charset" parameters in conjunction with subtypes of text.

Regardless of what approach is chosen, all new text/* registrations MUST clearly specify how the charset is determined; relying on the US-ASCII default defined in {{Section 4.1.2 of !RFC2046}} is no longer permitted. If explanatory text is needed, this SHOULD be placed in the additional information section of the registration.

Plain text does not provide for or allow formatting commands, font attribute specifications, processing instructions, interpretation directives, or content markup. Plain text is seen simply as a linear sequence of characters, possibly interrupted by line breaks or page breaks. Plain text MAY allow the stacking of several characters in the same position in the text. Plain text in scripts like Arabic and Hebrew may also include facilities that allow the arbitrary mixing of text segments with different writing directions.

Beyond plain text, there are many formats for representing what might be known as "rich text". An interesting characteristic of many such representations is that they are to some extent readable even without the software that interprets them. It is useful to distinguish them, at the highest level, from such unreadable data as images, audio, or text represented in an unreadable form. In the absence of appropriate interpretation software, it is reasonable to present subtypes of "text" to the user, while it is not reasonable to do so with most non-textual data. Such formatted textual data can be represented using subtypes of "text".

### Image Media Types

A top-level type of "image" indicates that the content specifies one or more individual images. The subtype names the specific image format.

### Audio Media Types

A top-level type of "audio" indicates that the content contains audio data. The subtype names the specific audio format.

### Video Media Types

A top-level type of "video" indicates that the content specifies a time-varying-picture image, possibly with color and coordinated sound. The term 'video' is used in its most generic sense, rather than with reference to any particular technology or format, and is not meant to preclude subtypes such as animated drawings encoded compactly.

Note that although in general the mixing of multiple kinds of media in a single body is discouraged {{!RFC2046}}, it is recognized that many video formats include a representation for synchronized audio and/or text, and this is explicitly permitted for subtypes of "video".

### Application Media Types

The "application" top-level type is to be used for discrete data that do not fit under any of the other type names, and particularly for data to be processed by some type of application program. This is information that must be processed by an application before it is viewable or usable by a user. Expected uses for the "application" type name include but are not limited to file transfer, spreadsheets, presentations, scheduling data, and languages for "active" (computational) material. (The last, in particular, can pose security problems that must be understood by implementors. The "application/postscript" media type registration in {{!RFC2046}} provides a good example of how to handle these issues.)

For example, a meeting scheduler might define a standard representation for information about proposed meeting dates. An intelligent user agent would use this information to conduct a dialog with the user, and might then send additional material based on that dialog. More generally, there have been several "active" languages developed in which programs in a suitably specialized language are transported to a remote location and automatically run in the recipient's environment. Such applications may be defined as subtypes of the "application" top-level type.

The subtype of "application" will often either be the name or include part of the name of the application for which the data are intended. This does not mean, however, that any application program name may simply be used freely as a subtype of "application"; the subtype needs to be registered.

### Multipart and Message Media Types

Multipart and message are composite types; that is, they provide a means of encapsulating zero or more objects, each one a separate media type.

All subtypes of multipart and message MUST conform to the syntax rules and other requirements specified in {{!RFC2046}} and amended by {{Section 3.5 of !RFC6532}}.

### Additional Top-Level Types

In some cases, a new media type may not "fit" under any currently defined top-level type names. Such cases are expected to be quite rare. However, if such a case does arise, a new type name can be defined to accommodate it. Definition of a new top-level type name MUST be done via a Standards Track RFC, taking into account the criteria and guidelines given below; no other mechanism can be used to define additional type names.

#### Required Criteria

The following is the list of required criteria for the definition of a new top-level type. Motivations for the requirements are also included.

* Every new top-level type MUST be defined in a Standards Track RFC (see {{Section 4.9 of !RFC8126}}). This will make sure there is sufficient community interest, review, and consensus appropriate for a new top-level type.

* The IANA Considerations section of an RFC defining a new top-level type MUST request that IANA add this new top-level type to the registry of top-level types.

* The criteria for what types do and do not fall under the new top-level type MUST be defined clearly. Clear criteria are expected to help expert reviewers to evaluate whether a subtype belongs below the new type or not, and whether the registration template for a subtype contains the appropriate information. If the criteria cannot be defined clearly, this is a strong indication that whatever is being talked about is not suitable as a top-level type.

* Any RFC defining a new top-level type MUST clearly document the security considerations applying to all or a significant subset of subtypes.

* At the minimum, one subtype MUST be described. A top-level type without any subtype serves no purpose. Please note that the 'example' top-level describes a subtype 'example'.

#### Additional Considerations

* Existing wide use of an unregistered top-level type may be an indication of a need, and therefore an argument for formally defining this new top-level type.

* On the other hand, the use of unregistered top-level types is highly discouraged.

* Use of an IETF Working Group to define a new top-level type is not needed, but may be advisable in some cases. There are examples of new top-level type definitions without a Working Group ({{?RFC2077}}), with a short, dedicated WG ({{?RFC8081}}), and with a Working Group that included other related work ({{?I-D.ietf-mediaman-haptics}}).

* The document defining the new top-level type should include initial registrations of actual subtypes. The exception may be a top-level type similar to 'example'. This will help to show the need for the new top-level type, will allow checking the appropriateness of the definition of the new top-level type, will avoid separate work for registering an initial slate of subtypes, and will provide examples of what is considered a valid subtype for future subtype registrations.

* The registration and actual use of a certain number of subtypes under the new top-level type should be expected. The existence of a single subtype should not be enough; it should be clear that new similar types may appear in the future. Otherwise, the creation of a new top-level type is most probably not justified.

* The proposers of the new top-level type and the wider community should be willing to commit to emitting and consuming the new top-level type in environments that they control.

* Desirability for common parameters: The fact that a group of (potential) types have (mostly) common parameters may be an indication that these belong under a common new top-level type.

* Top-level types can help humans with understanding and debugging. Therefore, evaluating how a new top-level type helps humans understand types may be crucial.

* Common restrictions may apply to all subtypes of a top-level type. Examples are the restriction to CRLF line endings for subtypes of type 'text' (at least in the context of electronic mail), or on subtypes of type 'multipart'.

* Top-level types are also used frequently in dispatching code. For example "multipart/*" is frequently handled as multipart/mixed, without understanding of a specific subtype. The top-level types 'image', 'audio', and 'video' are also often handled generically. Documents with these top-level types can be passed to applications handling a wide variety of image, audio, or video formats. HTML generating applications can select different HTML elements (e.g. \<img> or \<audio>) for including data of different top-level types. Applications can select different icons to represent unknown types in different top-level types.

#### Negative Criteria

This subsection lists negative criteria for top-level types, identifying criteria that are explicitly not reasons for a top-level type registration.

* A top-level type is not a pointer into another registration space that offers duplicate registrations for existing media types. Example: a top-level type of 'oid', leading to types of the form oid/nnnnn, where nnn is an OID (Object Identifier) designating a specific media format,

* A top-level type MUST NOT be defined for the mapping of other protocol elements to media types. For example, while there may be some merit to a mapping from media types to URIs, e.g. in the context of RDF (Resource Description Framework), there is very limited merit in a reverse mapping, and even less merit in creating a top-level type for such a mapping. The same applies to other protocol elements such as file extensions or URI schemes. The recommended solution in case a mapping is needed is to choose a single type/subtype and put the additional information in an appropriately named parameter. As an example, information on a file extension '.dcat' can be encoded as 'application/octet-string; filename=foo.dcat'.

* Media types are not a general type system. A top-level type MUST NOT be defined if its main or only purpose is to map other type systems, e.g. in programming languages or ontologies.

* A new top-level type SHOULD NOT generate aliases for existing widely used types or subtypes.

* Top-level types with an "X-" prefix cannot be registered, and SHOULD NOT be used. This is in line with {{!RFC6648}}.

### Structured Syntax Name Suffixes {#suffixes}

XML in MIME {{!RFC3023}} defined the first such augmentation to the media type definition to additionally specify the underlying structure of that media type. To quote:

> This document also standardizes a convention (using the suffix '+xml') for naming media types ... when those media types represent XML MIME (Multipurpose Internet Mail Extensions) entities.

That is, it specified a suffix (in that case, "+xml") to be appended to the base subtype name.

Since this was published, the de facto practice has arisen for using this suffix convention for other well-known structuring syntaxes. In particular, media types have been registered with suffixes such as "+der", "+fastinfoset", and "+json". This specification formalizes this practice and sets up a registry for structured type name suffixes.

The primary guideline for whether a structured type name suffix is registrable is that it be described by a readily available description, preferably within a document published by an established standards-related organization, and for which there's a reference that can be used in a Normative References section of an RFC.

Media types that make use of a named structured syntax SHOULD use the appropriate registered "+suffix" for that structured syntax when they are registered. By the same token, media types MUST NOT be given names incorporating suffixes for structured syntaxes they do not actually employ. "+suffix" constructs for as-yet unregistered structured syntaxes SHOULD NOT be used, given the possibility of conflicts with future suffix definitions.

### Deprecated Aliases {#deprecated-aliases}

In some cases, a single media type may have been widely deployed prior to registration under multiple names. In such cases, a preferred name MUST be chosen for the media type, and applications MUST use this to be compliant with the type's registration. However, a list of deprecated aliases by which the type is known MAY be supplied as additional information in order to assist applications in processing the media type properly.

## Parameter Requirements

Media types MAY elect to use one or more media type parameters, or some parameters may be automatically made available to the media type by virtue of being a subtype of a content type that defines a set of parameters applicable to any of its subtypes. In either case, the names, values, and meanings of any parameters MUST be fully specified when a media type is registered in the standards tree, and SHOULD be specified as completely as possible when media types are registered in the vendor or personal trees.

Parameter names have the syntax as media type names and values:

~~~ abnf
    parameter-name = restricted-name
~~~

Note that this syntax is somewhat more restrictive than what is allowed by the ABNF in {{!RFC2045}} and amended by {{?RFC2231}}.

Parameter names are case-insensitive and no meaning is attached to the order in which they appear. It is an error for a specific parameter to be specified more than once.

There is no defined syntax for parameter values. Therefore, registrations MUST specify parameter value syntax. Additionally, some transports impose restrictions on parameter value syntax, so care needs be taken to limit the use of potentially problematic syntaxes; e.g., pure binary valued parameters, while permitted in some protocols, are best avoided.

Note that a protocol can impose further restrictions on parameter value syntax, depending on how it chooses to represent parameters. Both MIME {{!RFC2045}} {{?RFC2231}} and HTTP {{!RFC2045}} {{?RFC5987}} allow binary parameters as well as parameter values expressed in a specific charset, but other protocols may be less flexible.

New parameters SHOULD NOT be defined as a way to introduce new functionality in types registered in the standards tree, although new parameters MAY be added to convey additional information that does not otherwise change existing functionality. An example of this would be a "revision" parameter to indicate a revision level of an external specification such as JPEG. Similar behavior is encouraged for media types registered in the vendor or personal trees, but is not required.

Changes to parameters (including the introduction of new ones) is managed in the same manner as other changes to the media type; see {{change}}.

## Canonicalization and Format Requirements

All registered media types MUST employ a single, canonical data format, regardless of registration tree.

A permanent and readily available public specification of the format for the media type MUST exist for all types registered in the standards tree. This specification MUST provide sufficient detail so that interoperability between independent implementations using the media type is possible. This specification MUST at a minimum be referenced by, if it is not actually included in, the media type registration proposal itself.

The specifications of format and processing particulars may or may not be publicly available for media types registered in the vendor and personal trees. Such registrations are explicitly permitted to limit the information in the registration to which software and version produce or process such media types. As such, references to or inclusion of format specifications in registrations is encouraged but not required. Note, however, that the public availability of a meaningful specification will often make the difference between simply having a name reserved so that there are no conflicts with other uses and having the potential for other implementations of the media type and useful interoperation with them.

Some media types involve the use of patented technology. The registration of media types involving patented technology is specifically permitted. However, the restrictions set forth in BCP 79 {{!RFC3979}} and BCP 78 {{!RFC5378}} on the use of patented technology in IETF Standards Track protocols must be respected when the specification of a media type is part of a Standards Track protocol. In addition, other standards-related organizations making use of the standards tree may have their own rules regarding intellectual property that must be observed in their registrations.

Intellectual Property Rights (IPR) disclosures for registrations in the vendor and personal trees are encouraged but not required.

## Interchange Recommendations

Ideally, media types will be defined so they interoperate across as many systems and applications as possible. However, some media types will inevitably have problems interoperating across different platforms. Problems with different versions, byte ordering, and specifics of gateway handling can and will arise.

Universal interoperability of media types is not required, but known interoperability issues SHOULD be identified whenever possible. Publication of a media type does not require an exhaustive review of interoperability, and the interoperability considerations section is subject to continuing evaluation.

The recommendations in this subsection apply regardless of the registration tree involved.

## Security Requirements {#secreq}

An analysis of security issues MUST be done for all types registered in the standards tree. A similar analysis for media types registered in the vendor or personal trees is encouraged but not required. However, regardless of what security analysis has or has not been done, all descriptions of security issues MUST be as accurate as possible regardless of registration tree. In particular, the security considerations MUST NOT state that there are "no security issues associated with this type". Security considerations for types in the vendor or personal tree MAY say that "the security issues associated with this type have not been assessed".

There is absolutely no requirement that media types registered in any tree be secure or completely free from risks. Nevertheless, all known security risks MUST be identified in the registration of a media type, again regardless of registration tree.

The security considerations section of all registrations is subject to continuing evaluation and modification, and in particular MAY be extended by use of the "comments on media types" mechanism described in {{comments}} below.

Some of the issues that need to be examined and described in a security analysis of a media type are:

* Complex media types may include provisions for directives that institute actions on a recipient's files or other resources. In many cases, provision is made for originators to specify arbitrary actions in an unrestricted fashion that may then have devastating effects. See the registration of the application/postscript media type in {{!RFC2046}} for an example of such directives and how they can be described in a media type registration.

* Any security analysis MUST state whether or not they employ such "active content"; if they do, they MUST state what steps have been taken, or MUST be taken by applications of the media type, to protect users of the media type from harm.

* Complex media types may include provisions for directives that institute actions that, while not directly harmful to the recipient, may result in disclosure of information that either facilitates a subsequent attack or else violates a recipient's privacy in some way. Again, the registration of the application/ postscript media type illustrates how such directives can be handled.

* A media type that employs compression may provide an opportunity for sending a small amount of data that, when received and evaluated, expands enormously to consume all of the recipient's resources. All media types SHOULD state whether or not they employ compression; if they do, they SHOULD discuss what steps need to be taken to avoid such attacks.

* A media type might be targeted for applications that require some sort of security assurance but don't provide the necessary security mechanisms themselves. For example, a media type could be defined for storage of sensitive medical information that in turn requires external confidentiality and integrity protection services, or which is designed for use only within a secure environment. Types SHOULD always document whether or not they need such services in their security considerations.

## Requirements Specific to XML Media Types

There are a number of additional requirements specific to the registration of XML media types. These requirements are specified in {{!RFC3023}}.

## Encoding Requirements {#encoding}

Some transports impose restrictions on the type of data they can carry. For example, Internet mail traditionally was limited to 7bit US-ASCII text. Encoding schemes are often used to work around such transport limitations.

It is therefore useful to note what sort of data a media type can consist of as part of its registration. An "encoding considerations" field is provided for this purpose. Possible values of this field are:

7bit:
: The content of the media type consists solely of CRLF- delimited 7bit US-ASCII text.

8bit:
: The content of the media type consists solely of CRLF- delimited 8bit text.

binary:
: The content consists of an unrestricted sequence of octets.

framed:
: The content consists of a series of frames or packets without internal framing or alignment indicators. Additional out- of-band information is needed to interpret the data properly, including but not necessarily limited to knowledge of the boundaries between successive frames and knowledge of the transport mechanism. Note that media types of this sort cannot simply be stored in a file or transported as a simple stream of octets; therefore, such media types are unsuitable for use in many traditional protocols. A commonly used transport with framed encoding is the Real-time Transport Protocol, RTP. Additional rules for framed encodings defined for transport using RTP are given in {{!RFC4855}}.

Additional restrictions on 7bit and 8bit text are given in {{Section 4.1.1 of !RFC2046}}.

## Usage and Implementation Non-Requirements {#non-requirements}

In the asynchronous mail environment, where information on the capabilities of the remote mail agent is frequently not available to the sender, maximum interoperability is attained by restricting the media types used to those "common" formats expected to be widely implemented. This was asserted in the past as a reason to limit the number of possible media types, and resulted in a registration process with a significant hurdle and delay for those registering media types.

However, the need for "common" media types does not require limiting the registration of new media types. If a limited set of media types is recommended for a particular application, that should be asserted by a separate applicability statement specific for the application and/or environment.

Therefore, universal support and implementation of a media type are NOT a requirement for registration. However, if a media type is explicitly intended for limited use, this MUST be noted in its registration. The "Restrictions on Usage" field is provided for this purpose.

## Publication Requirements

Media types registered in the standards tree by the IETF itself MUST be published as RFCs. RFC publication of vendor and personal media type registrations is allowed but not required. In all cases, the IANA will retain copies of all media type registrations and "publish" them as part of the media types registration tree itself.

As stated previously, standards-tree registrations for media types defined in documents produced by other standards-related organizations MUST be described by a formal standards specification produced by that organization. Additionally, any copyright on the registration template MUST allow the IANA to copy it into the IANA registry.

Other than IETF registrations in the standards tree, the registration of a media type does not imply endorsement, approval, or recommendation by the IANA or the IETF or even certification that the specification is adequate. To become an IETF standard, a protocol or data object must go through the IETF standards process. While it provides additional assurances when it is appropriate, this is too difficult and too lengthy a process for the convenient registration of media types.

The standards tree exists for media types that do require a substantive review and approval process in a recognized standards- related organization. The vendor and personal trees exist for those media types that do not require such a process. It is expected that applicability statements for particular applications will be published from time to time in the IETF, recommending implementation of, and support for, media types that have proven particularly useful in those contexts.

As discussed above, registration of a top-level type requires Standards Action in the IETF and, hence, the publication of a RFC on the Standards Track.

## Fragment Identifier Requirements

Media type registrations can specify how applications should interpret fragment identifiers (specified in {{Section 3.5 of !RFC3986}}) associated with the media type.

Media types are encouraged to adopt fragment identifier schemes that are used with semantically similar media types. In particular, media types that use a named structured syntax with a registered "+suffix" MUST follow whatever fragment identifier rules are given in the structured syntax suffix registration.

## Additional Information

Various sorts of optional information SHOULD be included in the specification of a media type if it is available:

* Magic number(s) (length, octet values). Magic numbers are byte sequences that are always present at a given place in the file and thus can be used to identify entities as being of a given media type.

* File name extension(s) commonly used on one or more platforms to indicate that some file contains a given media type.

* macOS Uniform Type Identifier (a string), if it makes sense to exchange media of this type through user-triggered exchange mechanisms such as copy-and-paste or drag-and-drop on macOS and related platforms (see {{MacOSUTIs}} for definitions and syntax).

* Windows clipboard name (a string), if it makes sense to exchange media of this type through user-triggered exchange mechanisms such as copy-and-paste or drag-and-drop on Microsoft Windows and related platforms (see {{windowsClipboardNames}} for definitions and syntax).

In the case of a registration in the standards tree, this additional information MAY be provided in the formal specification of the media type format. It is suggested that this be done by incorporating the IANA media type registration form into the format specification itself.

#  Media Type Registration Procedures {#procedures}

The media type registration procedure is not a formal standards process, but rather an administrative procedure intended to allow community comment and sanity checking without excessive time delay.

Normal IETF processes need to be followed for all IETF registrations in the standards tree. The posting of an Internet Draft is a necessary first step, followed by posting to the media-types@iana.org list as discussed below.

##  Preliminary Community Review {#preliminary-review}

Notice of a potential media type registration in the standards tree SHOULD be sent to the media-types@iana.org mailing list for review. This mailing list has been established for the purpose of reviewing proposed media and access types. Registrations in other trees MAY be sent to the list for review as well; doing so is entirely OPTIONAL, but is strongly encouraged.

The intent of the public posting to this list is to solicit comments and feedback on the choice of type/subtype name, the unambiguity of the references with respect to versions and external profiling information, and a review of any interoperability or security considerations. The submitter may submit a revised registration proposal or abandon the registration completely and at any time.

## Submit Request to IANA

Media types registered in the standards tree by the IETF itself MUST be reviewed and approved by the IESG as part of the normal standards process. Standards-tree registrations by recognized standards- related organizations as well as registrations in the vendor and personal trees are submitted directly to the IANA, unless other arrangements were made as part of a liaison agreement. In either case, posting the registration to the media-types@iana.org list for review prior to submission is strongly encouraged.

Registration requests can be sent to iana@iana.org. A web form for registration requests is also available:

> http://www.iana.org/form/media-types

### Provisional Registrations {#provisional}

Standardization processes often take considerable time to complete. In order to facilitate prototyping and testing, it is often helpful to assign identifiers, including but not limited to media types, early in the process. This way, identifiers used during standards development can remain unchanged once the process is complete, and implementations and documentation do not have to be updated.

Accordingly, a provisional registration process is provided to support early assignment of media type names in the standards tree. A provisional registration MAY be submitted to IANA for standards- tree types. The only required fields in such registrations are the media type name and contact information (including the standards- related organization name).

Upon receipt of a provisional registration, IANA will check the name and contact information, then publish the registration in a distinct publicly visible provisional registration list.

Provisional registrations MAY be updated or abandoned at any time. When the registration is abandoned, the media type is no longer registered in any sense; it can subsequently be registered just like any other unassigned media type name.

## Review and Approval

With the exception of provisional standards-tree registrations, registrations submitted to the IANA will be passed on to the media types reviewer. The media types reviewer, who is appointed by the IETF Applications Area Director(s), will review the registration to make sure it meets the requirements set forth in this document. Registrations that do not meet these requirements will be returned to the submitter for revision.

Decisions made by the media types reviewer may be appealed to the IESG using the procedure specified in {{Section 6.5.4 of ?RFC2026}}.

Once a media type registration has passed review, the IANA will register the media type and make the media type registration available to the community.

In the case of standards-tree registrations from other standards- related organizations, IANA will also check that the submitter is in fact a recognized standards-related organization. If the submitter is not currently recognized as such, the IESG will be asked to confirm their status. Recognition from the IESG MUST be obtained before a standards-tree registration can proceed.

## Comments on Media Type Registrations {#comments}

Comments on registered media types may be submitted by members of the community to the IANA at iana@iana.org. These comments will be reviewed by the media types reviewer and then passed on to the "owner" of the media type if possible. Submitters of comments may request that their comment be attached to the media type registration itself; if the IANA, in consultation with the media types reviewer, approves, the comment will be made accessible in conjunction with the type registration.

## Change Procedures {#change}

Once a media type has been published by the IANA, the owner may request a change to its definition. The descriptions of the different registration trees above designate the "owners" of each type of registration. The same procedure that would be appropriate for the original registration request is used to process a change request.

Media type registrations may not be deleted; media types that are no longer believed appropriate for use can be declared OBSOLETE by a change to their "intended use" field; such media types will be clearly marked in the lists published by the IANA.

Significant changes to a media type's definition should be requested only when there are serious omissions or errors in the published specification. When review is required, a change request may be denied if it renders entities that were valid under the previous definition invalid under the new definition.

The owner of a media type may pass responsibility to another person or agency by informing the IANA; this can be done without discussion or review.

The IESG may reassign responsibility for a media type. The most common case of this will be to enable changes to be made to types where the author of the registration has died, moved out of contact, or is otherwise unable to make changes that are important to the community.

## Registration Template

{:vspace}
Type name:
Subtype name:
Required parameters:
Optional parameters:
Encoding considerations:
Security considerations:
Interoperability considerations:
Published specification:
Applications that use this media type:
Fragment identifier considerations:
Additional information:
: Deprecated alias names for this type:

  Magic number(s):

  File extension(s):

  Macintosh file type code(s):
{:vspace}
Person & email address to contact for further information:
Intended usage:
: (One of COMMON, LIMITED USE, or OBSOLETE.)
{:vspace}
Restrictions on usage:
: (Any restrictions on where the media type can be used go here.)
{:vspace}
Author:
Change controller:
Provisional registration? (standards tree only):
: Yes/No

(Any other information that the author deems interesting may be added below this line.)

"N/A", written exactly that way, can be used in any field if desired to emphasize the fact that it does not apply or that the question was not omitted by accident. Do not use 'none' or other words that could be mistaken for a response.

Limited-use media types should also note in the applications list whether or not that list is exhaustive.

# Structured Syntax Suffix Registration Procedures {#suffix-procedures}

Someone wishing to define a "+suffix" name for a structured syntax for use with a new media type registration SHOULD:

1. Check IANA's registry of media type name suffixes to see whether or not there is already an entry for that well-defined structured syntax.

2. If there is no entry for their suffix scheme, fill out the template (specified in {{suffix-template}}) and include that with the media type registration. The template may be contained in an Internet Draft, alone or as part of some other protocol specification. The template may also be submitted in some other form (as part of another document or as a stand-alone document), but the contents will be treated as an "IETF Contribution" under the guidelines of BCP 78 {{!RFC5378}}.

3. Send a copy of the template or a pointer to the containing document (with specific reference to the section with the template) to the mailing list media-types@iana.org, requesting review. This may be combined with a request to review the media type registration. Allow a reasonable time for discussion and comments.

4. Respond to review comments and make revisions to the proposed registration as needed to bring it into line with the guidelines given in this document.

5. Submit the (possibly updated) registration template (or pointer to the document containing it) to IANA at iana@iana.org.

Upon receipt of a structured syntax suffix registration request,

1. IANA checks the submission for completeness; if sections are missing or citations are not correct, IANA rejects the registration request.

2. IANA checks the current registry for an entry with the same name; if such a registry exists, IANA rejects the registration request.

3. IANA requests Expert Review of the registration request against the corresponding guidelines.

4. The Designated Expert may request additional review or discussion, as necessary.

5. If Expert Review recommends registration, IANA adds the registration to the appropriate registry.

The initial registry content specification {{!RFC6839}} provides examples of structured syntax suffix registrations.

## Change Procedures

Registrations may be updated in each registry by the same mechanism as required for an initial registration. In cases where the original definition of the scheme is contained in an IESG-approved document, update of the specification also requires IESG approval.

## Structured Syntax Suffix Registration Template {#suffix-template}

This template describes the fields that must be supplied in a structured syntax suffix registration request:

{:vspace}
Name
: Full name of the well-defined structured syntax.

+suffix
: Suffix used to indicate conformance to the syntax.

References
: Include full citations for all specifications necessary to understand the structured syntax.

Encoding considerations
: General guidance regarding encoding considerations for any type employing this syntax should be given here. The same requirements for media type encoding considerations given in {{encoding}} apply here.

Interoperability considerations
: Any issues regarding the interoperable use of types employing this structured syntax should be given here. Examples would include the existence of incompatible versions of the syntax, issues combining certain charsets with the syntax, or incompatibilities with other types or protocols.

Fragment identifier considerations
: Generic processing of fragment identifiers for any type employing this syntax should be described here.

Security considerations
: Security considerations shared by media types employing this structured syntax must be specified here. The same requirements for media type security considerations given in {{secreq}} apply here, with the exception that the option of not assessing the security considerations is not available for suffix registrations.

Contact
: Person (including contact information) to contact for further information.

Author/Change controller.
: Person (including contact information) authorized to change this suffix registration.

# Security Considerations

Security requirements for both media type and media type suffix registrations are discussed in {{secreq}}.

# IANA Considerations

The purpose of this document is to define IANA registries for media types and structured syntax suffixes as well as the procedures for managing these registries. Additionally, this document requires IANA to maintain a list of standards-related organizations for which the IESG has approved media type registrations in the standards tree.

The existing media type registry has been extended to include a section for provisional registrations. Only standards-tree registrations are allowed in the standards tree and only at the request of an organization on the IANA list of standards-related organizations. See {{provisional}} for additional information on provisional registrations.

IANA has also added the following note at the top of the provisional registry:

> This registry, unlike some other provisional IANA registries, is only for temporary use. Entries in this registry are either finalized and moved to the main media types registry, or are abandoned and deleted. Entries in this registry are suitable for use for development and test purposes only.

The structured syntax name suffix registry has been created as follows:

* The name is the "Structured Syntax Suffix" registry.

* The registration process is specified in {{suffix-procedures}}.

* The information required for a registry entry as well as the entry format are specified in {{suffix-template}}.

* The initial content of the registry is specified in {{!RFC6839}}.

Entries in both the media type and structured suffix registries will be annotated by IANA with both the original registration date as well as the date of the most recent update to the entry. Registrations made prior to the implementation of this specification may, if necessary, be marked as such, rather than with a specific date.

Since registration entries can be updated multiple times, IANA will also maintain the history of changes to each registration in such a way that the state of the registration at any given time can be determined.

Finally, per this document, IANA has created a new email address, media-types@iana.org, for the media type review list, which replaces the ietf-types@iana.org address specified in RFC 4288. ietf-types@iana.org has been retained as an alias.

#  Acknowledgments

The current authors would like to acknowledge their debt to the late Dr. Jon Postel, whose general model of IANA registration procedures and specific contributions shaped the predecessors of this document {{?RFC2048}} {{?RFC4288}}. We hope that the current version is one with which he would have agreed but, as it is impossible to verify that agreement, we have regretfully removed his name as a co-author.

Randy Bush, Francis Dupont, Bjoern Hoehrmann, Barry Leiba, Murray Kucherawy, Alexey Melnikov, S. Moonesamy, Mark Nottingham, Tom Petch, Peter Saint-Andre, and Jeni Tennison provided many helpful review comments and suggestions.

--- back

# Grandfathered Media Types {#grandfather}

A number of media types with unfaceted subtype names, registered prior to 1996, would, if
registered under the guidelines in this document, be given a faceted name and placed into either
the vendor or personal trees. Reregistration of those types to reflect the appropriate trees is
encouraged but not required. Ownership and change control principles outlined in this document
apply to those types as if they had been registered in the trees described above.

From time to time there may also be cases where a media type with an unfaceted subtype name has
been widely deployed without being registered. (Note that this includes subtype names beginning
with the "x-" prefix.) If possible, such a media type SHOULD be reregistered with a proper faceted
subtype name, possibly using a deprecated alias to identify the original name (see {{deprecated-aliases}}).
However, if this is not possible, the type can, subject to approval by both the media types
reviewer and the IESG, be registered in the proper tree with its unfaceted name.


