# OpenEL

OpenEL(Open Embedded Library) is a unified API(Application Programming Interface) for actuators and sensors. The specifications and implementation have been developed by [JASA(Japan Embedded Systems Technology Association)](https://www.jasa.or.jp/data/english/) since 2011.

As of October 30, 2021, version 3.2 is available.

## 1. Scope

This specification specifies OpenEL, which defines the minimum common API(Application Program Interface) required for hardware devices(actuators and sensors) used in embedded systems.

This specification defines the Platform-Independent Model (PIM) of a Hardware Abstraction Layer(HAL) for embedded systems that is capable to support at least the following devices:

- Sensors. In addition to specifying the actual, normalized measurement, sensor kind and unit of measure shall be provided.
- Actuators. Commands to perform motions, and motion feedback information shall be provided.

In addition, this specification defines the Platform Specific Model (PSM) in language C based on the HAL PIM.
This specification aims to enable engineers such as application vendors and device vendors to build software without any concern about the differences among the targeted devices, by standardizing the API of these devices.

Target readers of this specification include:

- Software engineers who use the OpenEL to develop middleware and software.
- Device vendors and its engineers who develop devices and components which conforms to the OpenEL.
- Engineers who are interested in embedded software development.

## 2. Comformance

In order to comply with this specification, the following conditions must be satisfied.

- All devices must implement the component common definition excluding Actuator and Sensor element (section 7.4.1).

- Actuator device must implement at least one concrete Actuator class (Section 7.4.1.7).

- The sensor device must implement at least one concrete Sensor class (Section 7.4.1.8).

## 3. References

### 3.1 Normative References

The following normative documents contain provisions which, through reference in this text, constitute provisions of this specification. For dated references, subsequent amendments to, or revisions of, any of these publications do not apply.

[UML] [Object Management Group, OMG Unified Modeling Language (OMG UML)](https://www.omg.org/spec/UML/2.5.1/)

[ISO/IEC-9899] International Organization for Standardization, Programming languages - C, 1999

### 3.2 Non-normative References

- [Floating-Point Typedefs Having Specified Widths – N1703](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1703.pdf)

## 4. Terms and Definition

For the purposes of this specification, the following terms and definitions apply.

None

## 5. Symbols

[HAL] Hardware Abstraction Layer

[OpenEL] Open Embedded Library

## 6. Additional Information

None

## 7. Hardware Abstraction Layer for embedded system(OpenEL)

### 7.1 General

The Hardware Abstraction Layer for embedded system(OpenEL) is a standard specification for implementing control software systems. In OpenEL, to reduce constraints on implementers such as device vendors as much as possible, only the necessary minimum common API is specified.

It is a feature of embedded system that multiple devices operate in cooperation such as synchronous control of multiple actuators and measurement using multiple sensors, therefore this specification introduces the concept of "time".

By using the standardized API specified in this specification, portability and usability of various devices and drivers can be improved.
The use case and component diagram of OpenEL is shown below.

Note: HAL4RT is the standard name when JASA proposed standardization to OMG.

![Figure 7.1 Use case of OpenEL](images/image001.png "Use case of OpenEL")
Figure 7.1 Use case of OpenEL

![Figure 7.2 Architecture of OpenEL](images/image002.png "Architecture of OpenEL")
Figure 7.2 Architecture of OpenEL

## 7.2 Format and Conventions

### 7.2.1 Class and Interface

Classes and interfaces described in this PIM are documented using tables of the following format:

<p class=MsoCaption><span
style='font-size:10.0pt;font-family:"Times New Roman",serif'>Table x.x :
&lt;Class / Interface Name&gt;</span></p>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0
 style='border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:14.8pt'>
  <td width=672 colspan=6 valign=top style='width:503.7pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:14.8pt'>
  <p class=MsoNormal><b><span>Description</span></b><span
 > : &lt;description&gt;</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:14.8pt'>
  <td width=672 colspan=6 valign=top style='width:503.7pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:14.8pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: &lt;parent class&gt;</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=672 colspan=6 valign=top style='width:503.7pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=141 colspan=2 valign=top style='width:105.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName><span style='font-family:"Times New Roman",serif'>&lt;attribute
  name&gt;</span></p>
  </td>
  <td width=141 valign=top style='width:106.0pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;attribute
  type&gt;</span></p>
  </td>
  <td width=129 valign=top style='width:96.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;obligation&gt;</span></p>
  </td>
  <td width=103 valign=top style='width:77.55pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;occurrence&gt;</span></p>
  </td>
  <td width=156 valign=top style='width:117.35pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;description&gt;</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=141 colspan=2 valign=top style='width:105.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=141 style='width:106.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=129 style='width:96.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=103 style='width:77.55pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=156 style='width:117.35pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=672 colspan=6 valign=top style='width:503.7pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=141 colspan=2 valign=top style='width:105.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName><span
  style='font-family:"Times New Roman",serif'>&lt;operation
  name&gt;</span></p>
  </td>
  <td width=530 colspan=4 style='width:397.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;description&gt;</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=85 valign=top style='width:63.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName><span
  style='font-family:"Times New Roman",serif'>&lt;direction&gt;</span></p>
  </td>
  <td width=197 colspan=2 style='width:148.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;parameter name&gt;</span></p>
  </td>
  <td width=233 colspan=2 style='width:174.4pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;parameter type&gt;</span></p>
  </td>
  <td width=156 style='width:117.35pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>&lt;description&gt;</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=85 valign=top style='width:63.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=197 colspan=2 style='width:148.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=233 colspan=2 style='width:174.4pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
  <td width=156 style='width:117.35pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>…</span></p>
  </td>
 </tr>
 <tr height=0>
  <td width=85 style='border:none'></td>
  <td width=56 style='border:none'></td>
  <td width=141 style='border:none'></td>
  <td width=129 style='border:none'></td>
  <td width=103 style='border:none'></td>
  <td width=156 style='border:none'></td>
 </tr>
</table>

Note that derived attributes or operations are not described explicitly.

The ‘obligation’ and ‘occurrence’ are defined as follows.

#### Obligation

    M (mandatory): This attribute shall always be supplied.
    O (optional): This attribute may be supplied.
    C (conditional): This attribute shall be supplied under a condition. The condition is given as a part of the attribute description.

#### Occurrence

The occurrence column indicates the maximum number of occurrences of the attribute values that are permissible. The followings denote special meanings.

    N: No upper limit in the number of occurrences.
    ord: The appearance of the attribute values shall be ordered.
    unq: The appeared attribute values shall be unique.

### 7.2.2 Enumeration

Enumerations are documented as follows:

Table x.x: < enumeration name >

<table align="center">
    <tr>
        <td align="left">< constant name ></td>
        <td align="left">< description></td>
    </tr>
    <tr>
        <td align="left">...</td>
        <td align="left">...</td>
    </tr>
</table>

## 7.3 Return Codes

At the PIM level we have modeled errors as operation return codes typed __ReturnCode__. Each PSM may map these to either return codes or exceptions. The complete list of return codes is indicated below.

Table 7.1: ReturnCode enumeration

<table>
    <tr>
        <td align="left">HAL_OK</td>
        <td align="left">The operation completed successfully.</td>
    </tr>
    <tr>
        <td align="left">HAL_ERROR</td>
        <td align="left">An error occurred during execution of processing.</td>
    </tr>
</table>

## 7.4 Platform Independent Model (PIM)

### 7.4.1 Common definition

The common part defines a mechanism for managing devices. All the components need to implement the contents defined in the common part excluding Actuator and Sensor element. The class diagram of the common part is shown below.

![Figure 7.3 Common part](images/image003.png "Common part")
Figure 7.3 Common part

### 7.4.1.1 HALComponent

HALComponent is an element that holds information that all components should have in common.

It is possible to define a HALComponent with both Sensor and Actuator characteristics, such as cameras with gimbal mechanisms.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=672
 style='width:503.85pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=9
  colspan=2><p class='MsoNormal'>&nbsp;</td>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: None</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=4 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>halId</span></p>
  </td>
  <td width=103 colspan=3 style='width:77.45pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALId</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=53 colspan=2 style='width:39.75pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=361 colspan=2 style='width:270.9pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>ID
  for identifying the component.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=4 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>property</span></p>
  </td>
  <td width=103 colspan=3 style='width:77.45pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Property</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=53 colspan=2 style='width:39.75pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=361 colspan=2 style='width:270.9pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Details
  of the implementation content of each component.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=110 colspan=4 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>observerList</span></p>
  </td>
  <td width=103 colspan=3 style='width:77.45pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALObserver</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>O</span></p>
  </td>
  <td width=53 colspan=2 style='width:39.75pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>N</span></p>
  </td>
  <td width=361 colspan=2 style='width:270.9pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>A
  list of observers to notify upper-level applications of component-side
  information.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=4 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>time</span></p>
  </td>
  <td width=103 colspan=3 style='width:77.45pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>O</span></p>
  </td>
  <td width=53 colspan=2 style='width:39.75pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=361 colspan=2 style='width:270.9pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Component
  time information.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Time
  information of timer (OS timer, timer possessed by device, etc.) referenced
  by HALComponent.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>It
  is used to acquire data with time from a sensor without time information.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>The
  unit of time is implementation dependent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>Init</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Perform
  initialization processing of HALComponent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:19.85pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:19.85pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>ReInit</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:19.85pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Reset
  HALComponent. Reset error condition and return to normal state.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>Finalize</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Quit
  HAL Component.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>AddObserver</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Register
  an observer for notifying the event from the HALComponent to the upper
  application.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>target</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALObserver</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Observer
  to be registered.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>RemoveObserver</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Unregister
  observer set in HALComponent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>target</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALObserver</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Observer
  to be unregistered.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>GetProfile</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Acquire
  property information of HALComponent</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>profile</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Profile</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Profile
  information of HALComponent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>GetTime</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Get
  the time information of HALComponent. For components that do not have the
  time attribute, HAL_Error is returned.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>time</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Time
  information of HALComponent</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=1 style='border:none'></td>
  <td width=9 style='border:none'></td>
  <td width=37 style='border:none'></td>
  <td width=64 style='border:none'></td>
  <td width=23 style='border:none'></td>
  <td width=19 style='border:none'></td>
  <td width=61 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=17 style='border:none'></td>
  <td width=36 style='border:none'></td>
  <td width=2 style='border:none'></td>
  <td width=359 style='border:none'></td>
  <td width=1 style='border:none'></td>
  <td width=9 style='border:none'></td>
 </tr>
</table>

</div>

### State transition

The State Machine of the HAL Component is shown below. Note that state transitions specific to each device are defined within the "Active" state.

![Figure 7.4 State Machine of HALComponent](images/image004.png "State Machine of HALComponent")
Figure 7.4 State Machine of HALComponent

Details of each state are shown below.

- Initializing: A state in which device-specific processing is performed. Methods of HALComponent cannot be called.

- Initialized: The state where initialization of the device is completed. Only Init() is callable.

- Active: A state in which it is operating as a HALComponent. All APIs of HALComponent other than Init() and ReInit() can be called.

- Error: A state in which the operation is stopped due to an internal error etc. ReInit() and Finalize() can be called.

### 7.4.1.2 HALId

<p><span>HALId is an element representing the Id identifying
a HALComponent.</span></p>

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=672
 style='width:503.85pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=9><p class='MsoNormal'>&nbsp;</td>
  <td width=663 colspan=6 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: None</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=6 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>deviceKindId</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Identifier
  for identifying the type of device.<br>
  OMG performs management.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>vendorId</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Identifier
  for identifying the device vendor.<br>
  OMG performs management.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>productId</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Identifier
  for identifying the product.<br>
  The device vendor gives a unique numbering.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>instanceId</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>An
  identifier for identifying each device. When multiple products of the same
  type are used in the target system, they are used to identify them.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>The
  application creator sets in advance by some means.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=9 style='border:none'></td>
  <td width=101 style='border:none'></td>
  <td width=103 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=45 style='border:none'></td>
  <td width=369 style='border:none'></td>
  <td width=9 style='border:none'></td>
 </tr>
</table>

</div>

### 7.4.1.3 Property

Property is an element for holding details of the function of HALComponent.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=672
 style='width:503.85pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=9><p class='MsoNormal'>&nbsp;</td>
  <td width=663 colspan=6 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: None</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=6 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>id</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALId</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>An
  identifier representing the corresponding HALComponent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>deviceName</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>String</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Name
  of HALComponent.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid'>
  <td width=110 colspan=2 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>functionList</span></p>
  </td>
  <td width=103 style='width:77.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>String</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=45 style='width:33.6pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=369 style='width:277.05pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>List
  of function names implemented by HALComponent.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>When
  a device vendor adds and extends its own method, it describes which method is
  implemented by the target HALComponent. The whole image of the expanded
  original method is prepared by the device vendor with a spec sheet etc. The
  application creator shall know in advance what kind of extension method is
  defined.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=9 style='border:none'></td>
  <td width=101 style='border:none'></td>
  <td width=103 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=45 style='border:none'></td>
  <td width=369 style='border:none'></td>
  <td width=9 style='border:none'></td>
 </tr>
</table>

</div>

### 7.4.1.4 EventTimer

The EventTimer is an element used when synchronous control is performed for a plurality of HALComponents.

There are many kind of event timers (POSIX, proprietary RTOS, ... etc). The EventTimer unifies the APIs of different timers.

The EventTimer class is independent of HALComponent.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=672
 style='width:503.85pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=9
  colspan=2><p class='MsoNormal'>&nbsp;</td>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: None</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=110 colspan=4 style='width:82.75pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>observerList</span></p>
  </td>
  <td width=103 colspan=3 style='width:77.45pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>TimerObserver</span></p>
  </td>
  <td width=35 style='width:26.1pt;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>O</span></p>
  </td>
  <td width=45 colspan=2 style='width:33.6pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>N</span></p>
  </td>
  <td width=369 colspan=2 style='width:277.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>A
  list of observers to notify upper applications that the timer has timed out</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>StartTimer</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Start
  the event timer.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:19.85pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:19.85pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>StopTimer</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:19.85pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Stop
  the event timer.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>SetEventPeriod</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Set
  the event occurrence cycle.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>EventPeriod</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Event
  occurrence cycle</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>AddObserver</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Register
  an observer for notifying the timeout event from the EventTimer to the upper
  application.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>target</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Timer</span><span
  style='font-family:"Times New Roman",serif'>Observer</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Observer
  to be registered</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=6 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>RemoveObserver</span></p>
  </td>
  <td width=510 colspan=6 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Unregister
  the observer set in EventTimer.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 colspan=2 style='width:34.3pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 colspan=2 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>target</span></p>
  </td>
  <td width=132 colspan=4 style='width:99.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Timer</span><span
  style='font-family:"Times New Roman",serif'>Observer</span></p>
  </td>
  <td width=38 colspan=2 style='width:28.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=360 colspan=2 style='width:270.05pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Observer
  to be unregistered</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=1 style='border:none'></td>
  <td width=9 style='border:none'></td>
  <td width=37 style='border:none'></td>
  <td width=64 style='border:none'></td>
  <td width=23 style='border:none'></td>
  <td width=19 style='border:none'></td>
  <td width=61 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=17 style='border:none'></td>
  <td width=28 style='border:none'></td>
  <td width=10 style='border:none'></td>
  <td width=359 style='border:none'></td>
  <td width=1 style='border:none'></td>
  <td width=9 style='border:none'></td>
 </tr>
</table>

</div>

### 7.4.1.5 HALObserver

ALObserver is an interface for communicating the event occurrences in HALComponent to the application. For applications that use HALComponent, it is necessary to implement elements that realize this interface.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=663
 style='width:497.45pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=7 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=4 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>notify_event</span></p>
  </td>
  <td width=510 colspan=3 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Notify
  of an event occurred in HALComponent.</span></p>
  </td>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 style='width:34.3pt;border:solid windowtext 1.0pt;border-top:
  none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>source</span></p>
  </td>
  <td width=82 colspan=2 style='width:61.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALComponent</span></p>
  </td>
  <td width=38 style='width:10.0mm;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=410 colspan=2 style='width:307.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALComponent
  object that occurred the event.</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 style='width:34.3pt;border:solid windowtext 1.0pt;border-top:
  none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>event_id</span></p>
  </td>
  <td width=82 colspan=2 style='width:61.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=38 style='width:10.0mm;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=410 colspan=2 style='width:307.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>An
  identifier for distinguishing the type of event that has occurred.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>It
  is not an identifier for distinguishing individual events that have occurred.</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=4 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>notify_error</span></p>
  </td>
  <td width=510 colspan=3 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Notify
  of errors occurred in HALComponent.</span></p>
  </td>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 style='width:34.3pt;border:solid windowtext 1.0pt;border-top:
  none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>source</span></p>
  </td>
  <td width=82 colspan=2 style='width:61.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALComponent</span></p>
  </td>
  <td width=38 style='width:10.0mm;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=410 colspan=2 style='width:307.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>HALComponent
  object that occurred the error.</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 style='width:34.3pt;border:solid windowtext 1.0pt;border-top:
  none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>error_id</span></p>
  </td>
  <td width=82 colspan=2 style='width:61.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=38 style='width:10.0mm;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=410 colspan=2 style='width:307.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>An
  identifier to distinguish the type of error that occurred.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>It
  is not an identifier for distinguishing individual errors that have occurred.</span></p>
  </td>
 </tr>
 <tr height=0>
  <td width=0 style='border:none'></td>
  <td width=44 style='border:none'></td>
  <td width=85 style='border:none'></td>
  <td width=20 style='border:none'></td>
  <td width=84 style='border:none'></td>
  <td width=38 style='border:none'></td>
  <td width=390 style='border:none'></td>
  <td width=1 style='border:none'></td>
 </tr>
</table>

</div>

### 7.4.1.6 TimerObserver

TimerObserver is an interface for communicating the timeout event generated by the EventTimer to the application. Applications that use timer information, such as synchronous control of multiple actuators using EventTimer, need to implement elements that realize this interface.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=663
 style='width:497.45pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=7 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=152 colspan=4 style='width:114.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>notify_timer</span></p>
  </td>
  <td width=510 colspan=3 style='width:382.85pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Notify
  of timeout event generated by EventTimer.</span></p>
  </td>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=46 style='width:34.3pt;border:solid windowtext 1.0pt;border-top:
  none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=87 style='width:65.25pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>eventTimer</span></p>
  </td>
  <td width=82 colspan=2 style='width:61.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>EventTimer</span></p>
  </td>
  <td width=38 style='width:10.0mm;border-top:none;border-left:none;border-bottom:
  solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;padding:0mm 5.4pt 0mm 5.4pt;
  height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=410 colspan=2 style='width:307.3pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>EventTimer
  object that timed out.</span></p>
  </td>
 </tr>
 <tr height=0>
  <td width=1 style='border:none'></td>
  <td width=46 style='border:none'></td>
  <td width=87 style='border:none'></td>
  <td width=19 style='border:none'></td>
  <td width=64 style='border:none'></td>
  <td width=38 style='border:none'></td>
  <td width=409 style='border:none'></td>
  <td width=1 style='border:none'></td>
 </tr>
</table>

</div>

### 7.4.1.7 Actuator

The Actuator element defines the API that an Actuator device with one degree of freedom
should provide.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=675
 style='width:506.0pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=10
  colspan=2><p class='MsoNormal'>&nbsp;</td>
  <td width=665 colspan=12 style='width:498.75pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: HALComponent</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=666 colspan=12 style='width:499.4pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=121 colspan=4 style='width:90.8pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=69 colspan=3 style='width:51.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=37 colspan=2 style='width:28.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=54 colspan=2 style='width:40.85pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>NOrd</span></p>
  </td>
  <td width=384 style='width:288.3pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Actual value of the target actuator. If the
  actual angle / position / velocity / torque cannot be measured, estimated
  value or command value.</span></p>
  <p class=MsoNormal><span>Unit: [rad] or [m] / [rad/s] or [m/s] /
  [Nm] or [N]</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=666 colspan=12 style='width:499.4pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=124 colspan=5 style='width:92.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>GetValue</span></p>
  </td>
  <td width=542 colspan=7 style='width:406.55pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Obtain the actual angle / position /
  velocity / torque of the target actuator. If the actual angle / position /
  velocity / torque cannot be measured, return the estimated value or command
  value.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=56 colspan=2 style='width:42.15pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=97 colspan=3 style='width:72.95pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=60 colspan=2 style='width:45.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=54 colspan=2 style='width:40.65pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=398 colspan=3 style='width:298.2pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Actual actuator angle / position /
  velocity / torque.</span></p>
  <p class=MsoNormal><span>Unit: [rad] or [m] / [rad/s] or [m/s] /
  [Nm] or [N]</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=56 colspan=2 style='width:42.15pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=97 colspan=3 style='width:72.95pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>command</span></p>
  </td>
  <td width=60 colspan=2 style='width:45.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Enum</span></p>
  </td>
  <td width=54 colspan=2 style='width:40.65pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=398 colspan=3 style='width:298.2pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Actuator Controller mode.</span></p>
  <p class=MsoNormal><span>Command : POSITION / VELOCITY /</span><span
 > TORQUE</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=124 colspan=5 style='width:92.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>SetValue</span></p>
  </td>
  <td width=542 colspan=7 style='width:406.55pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Move the actuator to the target angle /
  position / velocity / torque.</span></p>
  <p class=MsoNormal><span>This method is asynchronous and does not
  wait until the actuator reaches the target angle / position / velocity /
  torque.</span></p>
  <p class=MsoNormal><span>If this method is called again before the
  actuator reaches the target angle / position / velocity / torque, the target
  angle / position / velocity / torque is updated.</span></p>
  <p class=MsoNormal><span>The fact that the actuator has reached
  the target angle / position / velocity / torque is notified to the
  application side using HALObserver. However, this notification is issued only
  when it reaches the final target angle / position / velocity / torque.
  Therefore, when this method is called a plurality of times and the target
  angle / position / velocity / torque is updated, only the notification
  corresponding to the method setting the final target angle / position /
  velocity / torque is performed.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=56 colspan=2 style='width:42.15pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=97 colspan=3 style='width:72.95pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=60 colspan=2 style='width:45.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=54 colspan=2 style='width:40.65pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=398 colspan=3 style='width:298.2pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Target angle / position / velocity /
  torque command.</span></p>
  <p class=MsoNormal><span>Unit: [rad] or [m] / [rad/s] or [m/s] /
  [Nm] or [N]</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=56 colspan=2 style='width:42.15pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>in</span></p>
  </td>
  <td width=97 colspan=3 style='width:72.95pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>command</span></p>
  </td>
  <td width=60 colspan=2 style='width:45.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=54 colspan=2 style='width:40.65pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>1</span></p>
  </td>
  <td width=398 colspan=3 style='width:298.2pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><span>Actuator Controller mode.</span></p>
  <p class=MsoNormal><span>Command : POSITION_CONTROL=1 / VELOCITY_CONTROL=2
  /</span><span> TORQUE_CONTROL=3</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=1 style='border:none'></td>
  <td width=8 style='border:none'></td>
  <td width=48 style='border:none'></td>
  <td width=64 style='border:none'></td>
  <td width=3 style='border:none'></td>
  <td width=31 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=25 style='border:none'></td>
  <td width=12 style='border:none'></td>
  <td width=42 style='border:none'></td>
  <td width=13 style='border:none'></td>
  <td width=384 style='border:none'></td>
  <td width=1 style='border:none'></td>
  <td width=8 style='border:none'></td>
 </tr>
</table>

</div>

The sample sequence diagram for synchronous control of multiple actuators using the API
defined above is shown below.

![Figure 7.5 The sample sequence diagram for synchronous control of multiple actuators.](images/image005.png "The sample sequence diagram for synchronous control of multiple actuators.")
Figure 7.5 The sample sequence diagram for synchronous control of multiple actuators.

![Figure 7.6 Execute the initialization process.](images/image006.png "Execute the initialization process.")
Figure 7.6 Execute the initialization process.

![Figure 7.7 Execute synchronous control.](images/image007.png "Execute synchronous control.")
Figure 7.7 Execute synchronous control.

### 7.4.1.8 Sensor

The Sensor element defines the API that a Sensor device should provide.

Like actuator devices, observers can be added and removed for sensor devices as well.

<div align=center>

<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=672
 style='width:503.85pt;border-collapse:collapse;border:none'>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=9
  colspan=2><p class='MsoNormal'>&nbsp;</td>
  <td width=663 colspan=12 style='width:496.95pt;border:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Derived From</span></b><span
 >: HALComponent</span></p>
  </td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:497.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Attributes</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=109 colspan=4 style='width:81.9pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName style='text-align:justify;text-justify:inter-ideograph'><span
  style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=102 colspan=3 style='width:76.4pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=35 style='width:25.95pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=56 colspan=2 style='width:42.2pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>NOrd</span></p>
  </td>
  <td width=361 colspan=2 style='width:270.65pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Measurement
  value of sensor device</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=663 colspan=12 style='width:497.1pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=MsoNormal><b><span>Operations</span></b></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=150 colspan=6 style='width:112.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>GetValue</span></p>
  </td>
  <td width=512 colspan=6 style='width:384.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Acquire sensor measurement value.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Used to acquire the sensor measurement value from the
  application side.</span></p>
  <p class=MsoNormal style='punctuation-wrap:hanging;text-autospace:ideograph-numeric ideograph-other'><span
 >The sensor measurement value is output in the
  International System of Units.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=45 colspan=2 style='width:34.0pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=86 colspan=2 style='width:64.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=131 colspan=4 style='width:98.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=49 colspan=2 style='width:36.8pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>NOrd</span></p>
  </td>
  <td width=352 colspan=2 style='width:263.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Sensor measurement value.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;border-bottom:solid windowtext 1.0pt' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=45 colspan=2 style='width:34.0pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=86 colspan=2 style='width:64.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>num</span></p>
  </td>
  <td width=131 colspan=4 style='width:98.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=49 colspan=2 style='width:36.8pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=352 colspan=2 style='width:263.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Number of value.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td width=150 colspan=6 style='width:112.85pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureName align=left style='text-align:left'><span
  style='font-family:"Times New Roman",serif'>GetTimedValue</span></p>
  </td>
  <td width=512 colspan=6 style='width:384.25pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Acquire sensor measurement value and measurement time.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Used to acquire the sensor measurement value from the
  application side. Time returns the time value defined by HALComponent.</span></p>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>The sensor measurement value is in the International System of
  Units.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=9 colspan=2><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=45 colspan=2 style='width:34.0pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=86 colspan=2 style='width:64.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>value</span></p>
  </td>
  <td width=131 colspan=4 style='width:98.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Real</span></p>
  </td>
  <td width=49 colspan=2 style='width:36.8pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>NOrd</span></p>
  </td>
  <td width=352 colspan=2 style='width:263.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Sensor measurement value.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=45 colspan=2 style='width:34.0pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=86 colspan=2 style='width:64.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>num</span></p>
  </td>
  <td width=131 colspan=4 style='width:98.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=49 colspan=2 style='width:36.8pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=352 colspan=2 style='width:263.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Number of value.</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr style='page-break-inside:avoid;height:16.15pt'>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=1><p class='MsoNormal'>&nbsp;</td>
  <td width=45 colspan=2 style='width:34.0pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span
  style='font-family:"Times New Roman",serif'>out</span></p>
  </td>
  <td width=86 colspan=2 style='width:64.45pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>time</span></p>
  </td>
  <td width=131 colspan=4 style='width:98.15pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Integer</span></p>
  </td>
  <td width=49 colspan=2 style='width:36.8pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>M</span></p>
  </td>
  <td width=352 colspan=2 style='width:263.75pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0mm 5.4pt 0mm 5.4pt;height:16.15pt'>
  <p class=FeatureValue><span style='font-family:"Times New Roman",serif'>Time value defined by HALComponent</span></p>
  </td>
  <td style='border:none;padding:0mm 0mm 0mm 0mm' width=8><p class='MsoNormal'>&nbsp;</td>
 </tr>
 <tr height=0>
  <td width=1 style='border:none'></td>
  <td width=9 style='border:none'></td>
  <td width=37 style='border:none'></td>
  <td width=63 style='border:none'></td>
  <td width=23 style='border:none'></td>
  <td width=19 style='border:none'></td>
  <td width=61 style='border:none'></td>
  <td width=35 style='border:none'></td>
  <td width=17 style='border:none'></td>
  <td width=39 style='border:none'></td>
  <td width=10 style='border:none'></td>
  <td width=351 style='border:none'></td>
  <td width=1 style='border:none'></td>
  <td width=8 style='border:none'></td>
 </tr>
</table>

</div>

The sample sequence diagram for synchronizing time information among multiple sensors using the API defined above is shown below.

![Figure 7.8 Execute synchronous control of multiple sensors.](images/image008.png "Execute synchronous control of multiple sensors.")
Figure 7.8 Execute synchronous control of multiple sensors.

## 7.5 Platform Specific Model(PSM)

This section specifies the PSM for OpenEL. OpenEL offers only one PSM, which is based on the ISO/IEC 9899:1999 Programming Language C (also known as C99).

### 7.5.1 PIM-PSM mapping rule

The mapping rules between PIM and PSM are shown below.
- PIM classes are mapped to C structures.
- PIM interfaces are mapped to C functions.
- PIM enumerated types are mapped to C enums or macro.
- Since it is difficult to realize generalization in C, implement the contents defined in all superclasses in the lowest
subclass.
-  The out-type argument of each method is mapped to a pointer.

### 7.5.2 Type Definition

Primitive types used in PIM are mapped to the following types respectively.
-  Integer: int32_t
- String: pointer
- Real: halfloat(float32_t or float64_t)
Also, for elements with multiplicity of *, map to pointer.

### 7.5.3 C PSM

**Note**:

The correct (system-specific) header file defining sized types (here: int32_t) must be included.

In macOS and probably other BSD-based systems that would be:

`#include </usr/include/sys/types.h>`

In many Linux systems this would be:

`#include </usr/include/stdint.h>`

But the actual path and header name may vary from system to system

```
/* ==================================================
* IMPORTANT - You need to inlude the system-specific header file
* that defines type "int32_t" here.
* ================================================== */

#ifndef HAL4RT_H
#define HAL4RT_H

#ifdef __cplusplus
namespace hal {
extern "C" {
#endif /* __cplusplus */

enum ReturnCode {
  HAL_OK = 0,
  HAL_ERROR
};

/* typedef definition */
typedef float  float32_t;
typedef double float64_t;
#if HAL_SW_FLOAT_SIZE
  typedef float32_t HALFLOAT_T;
#else
  typedef float64_t HALFLOAT_T;
#endif

typedef struct HalLinkedList_st {
        struct HalLinkedList_st *pNext;
} HAL_LINKED_LIST_T;

#define HAL_LINKED_LIST_HEAD HAL_LINKED_LIST_T linkedList;

typedef struct HalID_st {
  int32_t deviceKindId;
	int32_t vendorId;
	int32_t productId;
	int32_t instanceId;
} HALID_T;

typedef struct HalProperty_st {
	char *deviceName;
	char **sizeFunctionList;
} HALPROPERTY_T;

typedef struct HalComponent_st HALCOMPONENT_T;

typedef struct HALObserver {
	HAL_LINKED_LIST_HEAD
  void (*notify_event)(HALCOMPONENT_T *halComponent, int32_t eventId);
	void (*notify_error)(HALCOMPONENT_T *halComponent, int32_t errorId);
} HALOBSERVER_T;

#define HALCOMPONENT_BASE_MEMBER \
	int32_t handle; \
	HALID_T halId;\
	HALPROPERTY_T *property;\
	HALOBSERVER_T *observerList;\
	int32_t time;

typedef struct HalComponent_st {
	HALCOMPONENT_BASE_MEMBER
} HALCOMPONENT_T;

enum ReturnCode HalInit(HALCOMPONENT_T *halComponent);
enum ReturnCode HalReInit(HALCOMPONENT_T *halComponent);
enum ReturnCode HalFinalize(HALCOMPONENT_T *halComponent);
enum ReturnCode HalAddObserver(HALCOMPONENT_T *halComponent, HALOBSERVER_T *halObserver);
enum ReturnCode HalRemoveObserver(HALCOMPONENT_T *halComponent, HALOBSERVER_T *halObserver);
enum ReturnCode HalGetProperty(HALCOMPONENT_T *halComponent, HALPROPERTY_T *property);
enum ReturnCode HalGetTime(HALCOMPONENT_T *halComponent, int32_t *time_value);

typedef struct HalEventTimer_st HALEVENTTIMER_T;

typedef struct HalTimerObserver_st {
  HAL_LINKED_LIST_HEAD
  void (*notify_timer)(EVENTTIMER_T *eventTimer);
} HALTIMEROBSERVER_T;

typedef struct HalEventTimer_st {
  TIMEROBSERVER_T *observerList;
  int32_t eventPeriod;
} HALEVENTTIMER_T;

enum ReturnCode HalEventTimerStartTimer(EVENTTIMER_T *eventTimer);
enum ReturnCode HalEventTimerStopTimer(EVENTTIMER_T *eventTimer);
enum ReturnCode HalEventTimerSetEventPeriod(EVENTTIMER_T *eventTimer, int32_t eventPeriod);
enum ReturnCode HalEventTimerAddObserver(EVENTTIMER_T *eventTimer, TIMEROBSERVER_T *timerObserver);
enum ReturnCode HalEventTimerRemoveObserver(EVENTTIMER_T *eventTimer, TIMEROBSERVER_T *timerObserver);

typedef struct Actuator_st {
  /* HALCOMPONENT */
  HALCOMPONENT_BASE_MEMBER
  /* ACTUATOR */
  HALFLOAT_T *valueList;
} ACTUATOR_T;

#define HAL_REQUEST_POSITION_CONTROL   (1)
#define HAL_REQUEST_VELOCITY_CONTROL    (2)
#define HAL_REQUEST_TORQUE_CONTROL      (3)

enum ReturnCode HalMotorSetCommandValue(HALCOMPONENT_T *halComponent, int32_t request, HALFLOAT_T value);
enum ReturnCode HalMotorGetActualValue(HALCOMPONENT_T *halComponent, int32_t request, HALFLOAT_T *value);

typedef struct Sensor_st {
  /* HALCOMPONENT */
  HALCOMPONENT_BASE_MEMBER
  /* SENSOR */
  HALFLOAT_T *valueList;
} SENSOR_T;

enum ReturnCode HalSensorGetValueList(HALCOMPONENT_T *halComponent, int32_t *num, HALFLOAT_T *list);
enum ReturnCode HalSensorGetTimedValueList(HALCOMPONENT_T *halComponent, int32_t *num, HALFLOAT_T *list, int32_t *time);

#ifdef __cplusplus
} /* extern "C" */
} /* namespace hal */
#endif /* __cplusplus */

#endif /* HAL4RT_H */
```

