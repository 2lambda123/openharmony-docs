# Linux Kernel Overview


OpenHarmony adopts the Linux kernel as the basic kernel for standard-system devices \(reference memory ≥ 128 MiB\)  so that appropriate OS kernels can be selected for the devices subject to resource limitations and therefore provide basic capabilities for upper-layer apps.

## Linux Kernel Versions

Linux kernel versions are classified into the stable version and long-term support \(LTS\) version.

The stable version is released approximately every 3 months to support the latest hardware, improve performance, and fix bugs. Its disadvantage is that the overall maintenance lifespan is short, making long-term stable support unavailable for software.

The LTS version provides long-term kernel maintenance \(in fixing bugs and security vulnerabilities\). Generally, the maintenance lifespan is six years. By contrast, non-LTS kernel versions whose maintenance lifespan ranges from six months to two years cannot cover the entire lifespan of their products and may leave the products open to security vulnerabilities. In addition, new features are not added in the LTS version update, which ensures the version stability. Therefore, LTS versions are more suitable for commercial products that pursue stability and security.

## OpenHarmony Kernel Version Selection

The Linux kernel in OpenHarmony selects appropriate LTS versions as its basic versions. Currently, it supports Linux-4.19 and Linux-5.10.

