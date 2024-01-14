# ARM Trust Zone
Execution modes and privilege levels:\
![trust zone execution modes and privilege levels](/pictures/tz-exec-mode-s-ns.svg)

Trustzone-A also has a so-called Security Monitor, which is the **sole entry point** into secure world.\
Trustzone-M processors can have **many entry points**, which are placed in a dedicated region, called non-secure callable region.

There are three security attributes a memory region can have. One for each security level (secure and non-secure) and an additional (non-secure callable), which we are going to discuss soon:
- non-secure (**NS**)
- non-secure callable (**NSC**)
- secure (**S**)

## Banked Registers
Between security states the following registers are banked. 
Banking a register means that there are distinct instances of these registers available. 
These instances are switched automatically by the core during transitioning from NS to S and back. 
The following registers are banked in Armv8-M:

Banked general-purpose registers:
- `R13`: `SP` (Stack Pointer)
Banked special-purpose registers:
- `PRIMASK`, `FAULTMASK`, `BASEPRI`
- Some bits in `CONTROL`
The System Control Space `SCS` is also banked.

## SAU & IDAU: Security Attribution
Security attribution of memory addresses is done in so-called Attribution Units:
- Security Attribution Unit (SAU), which is always available in Armv8-M cores. On reset SAU is disabled.
- Implementation Defined Attribution Unit (IDAU), which is external to the core and the presence depends on the vendors implementation.

# TF-M
Trusted Firmware-M (TF-M) implements the Secure Processing Environment (SPE) for Armv8-M, Armv8.1-M architectures (e.g. the Cortex-M33, Cortex-M23, Cortex-M55, Cortex-M85 processors) and dual-core platforms.
It is the platform security architecture reference implementation aligning with PSA Certified guidelines, enabling chips, Real Time Operating Systems and devices to become PSA Certified.

TF-M relies on an isolation boundary between the Non-secure Processing Environment (NSPE) and the Secure Processing Environment (SPE). 
It can but is not limited to using the Arm TrustZone technology on Armv8-M and Armv8.1-M architectures. 
In pre-Armv8-M architectures physical core isolation is required.
TF-M consists of:
- Secure Boot to authenticate NSPE and SPE images
- TF-M Core for controlling the isolation, communication and execution within SPE and with NSPE
-Crypto, Internal Trusted Storage (ITS), Protected Storage (PS), Firmware Update and Attestation secure services

![tf-m armv8](/pictures/readme_tfm_v8.png)

TBSA-M means Trusted Base Architecture M 

Applications and Libraries in the Non-secure Processing Environment can utilize these secure services with a standardized set of PSA Functional APIs. 
Applications running on Cortex-M devices can leverage TF-M services to ensure secure connection with edge gateways and IoT cloud services. 
It also protects the critical security assets such as sensitive data, keys and certificates on the platform.
TF-M is supported on several Cortex-M based Microcontrollers and Real Time Operating Systems (RTOS).
[source](https://ci-builds.trustedfirmware.org/static-files/31168MMjuHf7gsU-9MGWjKtZQh70dGofYDViYgHrvqoxNjk5ODYxNTc2MjQ3Ojk6YW5vbnltb3VzOmpvYi90Zi1tLWJ1aWxkLWRvY3MtbmlnaHRseS9sYXN0U3RhYmxlQnVpbGQvYXJ0aWZhY3Q=/trusted-firmware-m/build/docs/user_guide/html/introduction/readme.html)

# Platform Security Architecture (PSA)
