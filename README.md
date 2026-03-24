# nsx-spi

`nsx-spi` provides an optional NSX wrapper for Ambiq SPI usage.

Purpose:
- preserve a migration-friendly `ns_spi_*` API surface
- hide family-specific or board-specific SPI details behind one module
- support future sensor or device drivers that want an NSX-managed SPI layer

This module depends on the existing NSX shim layers used by migrated legacy bus
code and remains optional by design.
