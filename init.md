## Walkthrough of FreeBSD 14.2's Boot Code

#### mi\_startup (sys/kern/init\_main.c:260)

```txt
Control Flow:
mi_startup <-- Here
```

### SI\_SUB\_TUNABLES

#### madt\_register (sys/x86/acpica/madt.c:325)

```txt
Control Flow:
mi_startup
    ...
    madt_register <-- Here

Note: madt_enumerator is defined on lines 92-98
      of sys/x86/acpica/madt.c.
```

#### x86\_iommu\_set\_intel (sys/x86/iommu/intel\_drv.c:1330)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel <-- Here
```

#### mptable\_register (sys/x86/x86/mptable.c:472)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register <-- Here
```

#### apic\_init (sys/x86/x86/local\_apic.c:1843)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init <-- Here
```

#### acpi\_set\_debugging (sys/dev/acpica/acpi.c:4382)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging <-- Here
```

#### mp\_setmaxid (sys/kern/subr\_smp.c:142)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging
    mp_setmaxid <-- Here
```

#### tunable\_set\_numzones (sys/kern/kern\_malloc.c:308)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging
    mp_setmaxid
    tunable_set_numzones <-- Here
```

#### init\_maxsockets (sys/kern/uipc\_socket.c:733)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging
    mp_setmaxid
    tunable_set_numzones
    init_maxsockets <-- Here
```

#### inittimehands (sys/kern/kern\_tc.c:1974)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging
    mp_setmaxid
    tunable_set_numzones
    init_maxsockets
    inittimehands <-- Here
```

#### init\_scsi\_delay (sys/cam/scsi/scsi\_all.c:9383)

```txt
Control Flow:
mi_startup
    ...
    madt_register
    x86_iommu_set_intel
    mptable_register
    apic_init
    acpi_set_debugging
    mp_setmaxid
    tunable_set_numzones
    init_maxsockets
    inittimehands
    init_scsi_delay <-- Here
```

### SI\_SUB\_COPYRIGHT

#### print\_caddr\_t (sys/kern/init\_main.c:352)

```txt
Control Flow:
mi_startup
    ...
    print_caddr_t <-- Here
```

#### print\_version (sys/kern/init\_main.c:358)

```txt
Control Flow:
mi_startup
    ...
    print_caddr_t
    print_version <-- Here
```

#### cap\_rights\_sysinit (sys/kern/subr\_capability.c:101)

```txt
Control Flow:
mi_startup
    ...
    print_caddr_t
    print_version
    cap_rights_sysinit <-- Here
```

### SI\_SUB\_VM

#### vm\_stats\_init (sys/vm/vm\_meter.c:559)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init <-- Here
```

#### uma\_startup3 (sys/vm/uma\_core.c:3204

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3 <-- Here
```

#### max\_ldt\_segment\_init (sys/amd64/amd64/sys\_machdep.c:82)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment_init <-- Here
```

#### vm\_page\_init\_cache\_zones (sys/vm/vm\_page.c:211)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment_init
    vm_page_init_cache_zones <-- Here
```

#### ffs\_rawread\_setup (sys/ufs/ffs/ffs\_rawread.c:83)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment_init
    vm_page_init_cache_zones
    ffs_rawread_setup <-- Here
```

### SI\_SUB\_COUNTER

#### pcpu\_zones\_startup (sys/kern/subr\_pcpu.c:143)

```txt
Control Flow:
mi_startup
    ...
    pcpu_zones_startup <-- Here
```

#### uma\_startup\_pcpu (sys/vm/uma\_core.c:3192)

```txt
Control Flow:
mi_startup
    ...
    pcpu_zones_startup
    uma_startup_pcpu <-- Here
```

#### cryptostats\_init (sys/opencrypto/crypto.c:231)

```txt
Control Flow:
mi_startup
    ...
    pcpu_zones_startup
    uma_startup_pcpu
    cryptostats_init <-- Here
```

### SI\_SUB\_KMEM

#### sysctl\_register\_all (sys/kern/kern\_sysctl.c:959)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all <-- Here
```

#### vmcounter\_startup (sys/vm/vm\_meter.c:101)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup <-- Here
```

#### mallocinit (sys/kern/kern\_malloc.c:1268)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit <-- Here
```

#### tunable\_mbinit (sys/kern/kern\_mbuf.c:153)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit <-- Here
```

#### ktr\_entries\_initializer (sys/kern/kern\_ktr.c:186)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer <-- Here
```

#### sleepinit (sys/kern/kern\_synch.c:104)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit <-- Here
```

#### pmap\_bootstrap\_la57 (sys/amd64/amd64/pmap.c:2172)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57 <-- Here
```

#### kstack\_cache\_init (sys/vm/vm\_glue.c:462)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init <-- Here
```

#### vt\_update\_static (sys/dev/vt/vt\_core.c:282)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static <-- Here
```

#### vt\_init\_font (sys/dev/vt/vt\_core.c:1792)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font <-- Here
```

#### vid\_malloc\_init (sys/dev/fb/fb.c:103)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init <-- Here

105: vid_malloc = TRUE;
```

#### xrefinfo\_init (sys/dev/ofw/openfirm.c:142)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init <-- Here
```

#### sysctl\_register\_fdt\_oid (sys/dev/ofw/ofw\_fdt.c:125)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid <-- Here
```

#### scmeminit (sys/dev/syscons/syscons.c:675)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit <-- Here
```

#### authunix\_init (sys/rpc/auth\_unix.c:111)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init <-- Here
```

#### rpc\_gss\_hashinit (sys/rpc/rpcsec\_gss/rpcsec\_gss.c:163)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit <-- Here
```

#### authtls\_init (sys/rpc/rpcsec\_tls/auth\_tls.c:89)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit
    authtls_init <-- Here
```

#### authnone\_init (sys/rpc/auth\_none.c:88)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit
    authtls_init
    authnone_init <-- Here
```

#### init\_dynamic\_kenv (sys/kern/kern\_environment.c:456)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit
    authtls_init
    authnone_init
    init_dynamic_kenv <-- Here
```

#### static\_hints\_to\_env (sys/kern/subr\_hints.c:59)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit
    authtls_init
    authnone_init
    init_dynamic_kenv
    static_hints_to_env <-- Here
```

#### fetch\_loader\_passphrase (sys/geom/eli/g\_eli.c:153)

```txt
Control Flow:
mi_startup
    ...
    sysctl_register_all
    vmcounter_startup
    mallocinit
    tunable_mbinit
    ktr_entries_initializer
    sleepinit
    pmap_bootstrap_la57
    kstack_cache_init
    vt_update_static
    vt_init_font
    vid_malloc_init
    xrefinfo_init
    sysctl_register_fdt_oid
    scmeminit
    authunix_init
    rpc_gss_hashinit
    authtls_init
    authnone_init
    init_dynamic_kenv
    static_hints_to_env
    fetch_loader_passphrase <-- Here
```

### SI\_SUB\_HYPERVISOR

#### xen\_hvm\_sysinit (sys/x86/xen/hvm.c:407)

```txt
Control Flow:
mi_startup
    ...
    xen_hvm_sysinit <-- Here
```

#### hyperv\_init (sys/dev/hyperv/vmbus/hyperv.c:175)

```txt
Control Flow:
mi_startup
    ...
    hyperv_init <-- Here
```

### SI\_SUB\_MTX\_POOL\_DYNAMIC

#### mtx\_pool\_setup\_dynamic (sys/kern/kern\_mtxpool.c:)

```txt
Control Flow:
mi_startup
    ...
    mtx_pool_setup_dynamic <-- Here
```

### SI\_SUB\_LOCK

#### lf\_init (sys/kern/kern\_lockf.c:280)

```txt
Control Flow:
mi_startup
    ...
    lf_init <-- Here
```

#### filelistinit (sys/kern/kern\_descrip.c:5165)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit <-- Here
```

#### nlm\_client\_init (sys/nlm/nlm\_advlock.c:96)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init <-- Here
```

#### ena\_lock\_init (sys/dev/ena/ena.c:4159)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init <-- Here
```

#### udl\_buffer\_init (sys/dev/usb/video/udl.c:184)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init <-- Here
```

#### usb\_quirk\_init (sys/dev/usb/quirk/usb\_quirk.c:1088)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init <-- Here
```

#### cdceem\_init (template/usb\_template\_cdceem.c:201)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init <-- Here
```

#### kbd\_init (template/usb\_template\_kbd.c:237)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init <-- Here
```

#### midi\_init (template/usb\_template\_midi.c:258)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init <-- Here
```

#### modem\_init (template/usb\_template\_modem.c:272)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init <-- Here
```

#### audio\_init (template/usb\_template\_audio.c:412)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init <-- Here
```

#### phone\_init (template/usb\_template\_phone.c:430)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init <-- Here
```

#### eth\_init (template/usb\_template\_cdce.c:279)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init <-- Here
```

#### usb\_temp\_init (template/usb\_template.c:1464)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init <-- Here
```

#### serialnet\_init (template/usb\_template\_serialnet.c:386)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init <-- Here
```

#### multi\_init (template/usb\_template\_multi.c:430)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init <-- Here
```

#### mtp\_init (template/usb\_template\_mtp.c:267)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init <-- Here
```

#### msc\_init (template/usb\_template\_msc.c:200)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init <-- Here
```

#### mouse\_init (template/usb\_template\_mouse.c:235)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init <-- Here
```

#### hidquirk\_init (sys/dev/hid/hidquirk.c:404)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init <-- Here
```

#### atomic64\_mtxinit (sys/kern/subr\_atomic64.c:137)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit <-- Here
```

#### init\_sleepqueue\_profiling (sys/kern/subr\_sleepqueue.c:188)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling <-- Here
```

#### kobj\_init\_mutex (sys/kern/subr\_kobj.c:72)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex <-- Here
```

#### init\_bounce\_pages (sys/kern/subr\_busdma\_bounce.c:132)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages <-- Here
```

#### rangelock\_sys\_init (sys/kern/kern\_rangelock.c:49)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init <-- Here
```

#### rs\_rangeset\_init (sys/kern/subr\_rangeset.c:48)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init <-- Here
```

#### osd\_init (sys/kern/kern\_osd.c:421)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init <-- Here
```

#### init\_turnstile\_profiling (sys/kern/subr\_turnstile.c:398)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init
    init_turnstile_profiling <-- Here
```

#### init\_turnstile0 (sys/kern/subr\_turnstile.c:423)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init
    init_turnstile_profiling
    init_turnstile0 <-- Here
```


#### ald\_startup (sys/kern/kern\_alq.c:183)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init
    init_turnstile_profiling
    ald_startup <-- Here
```

#### crc32c\_init\_hw (sys/libkern/x86/crc32\_sse42.c:203)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init
    init_turnstile_profiling
    ald_startup
    crc32c_init_hw <-- Here
```

#### chacha20\_init (sys/libkern/arc4random.c:160)

```txt
Control Flow:
mi_startup
    ...
    lf_init
    filelistinit
    nlm_client_init
    ena_lock_init
    udl_buffer_init
    usb_quirk_init
    cdceem_init
    kbd_init
    midi_init
    modem_init
    audio_init
    phone_init
    eth_init
    usb_temp_init
    serialnet_init
    multi_init
    mtp_init
    msc_init
    mouse_init
    hidquirk_init
    atomic64_mtxinit
    init_sleepqueue_profiling
    kobj_init_mutex
    init_bounce_pages
    rangelock_sys_init
    rs_rangeset_init
    osd_init
    init_turnstile_profiling
    ald_startup
    crc32c_init_hw
    chacha20_init <-- Here
```

### SI\_SUB\_EVENTHANDLER

#### eventhandler\_init (sys/kern/subr\_eventhandler.c:59)

```txt
Control Flow:
mi_startup
    ...
    eventhandler_init <-- Here
```

#### gcov\_init (sys/gnu/gcov/gcov\_subr.c:153)

```txt
Control Flow:
mi_startup
    ...
    eventhandler_init
    gcov_init <-- Here
```

#### umtxq\_sysinit (sys/kern/kern\_umtx.c:324)

```txt
Control Flow:
mi_startup
    ...
    eventhandler_init
    gcov_init
    umtxq_sysinit <-- Here
```

#### dn\_evh\_init (sys/net/debugnet.c:919)

```txt
Control Flow:
mi_startup
    ...
    eventhandler_init
    gcov_init
    umtxq_sysinit
    dn_evh_init <-- Here
```

### SI\_SUB\_VNET\_PRELINK

#### vnet\_init\_prelink (sys/net/vnet.c:310)

```txt
Control Flow:
mi_startup
    ...
    vnet_init_prelink <-- Here
```

### SI\_SUB\_KLD

#### ipoib\_unrhdr\_init (infiniband/ulp/ipoib/ipoib\_main.c:100)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init <-- Here
```

#### ucom\_init (usb/serial/usb\_serial.c:197)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init <-- Here
```

#### linker\_init (sys/kern/kern\_linker.c:157)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init <-- Here
```

#### dpcpu\_startup (sys/kern/subr\_pcpu.c:121)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup <-- Here
```

#### module\_init (sys/kern/kern\_module.c:81)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init <-- Here
```

#### vnet\_data\_startup (sys/net/vnet.c:350)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup <-- Here
```

#### usb\_dev\_init (usb/usb\_dev.c:964)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init <-- Here
```

#### link\_elf\_init (sys/kern/link\_elf\_obj.c:203)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init <-- Here
```

#### link\_elf\_init (sys/kern/link\_elf.c:435)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init <-- Here
```

#### linker\_preload (sys/kern/kern\_linker.c:1573)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload <-- Here
```

#### drm\_magic\_init (sys/dev/drm2/drm\_auth.c:199)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init <-- Here
```

#### drm\_core\_init (sys/dev/drm2/drm\_drv.c:255)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init
    drm_core_init <-- Here
```

#### linker\_stop\_class\_add (sys/kern/kern\_linker.c:168)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init
    drm_core_init
    linker_stop_class_add <-- Here
```

#### linker\_init\_kernel\_modules (sys/kern/kern\_linker.c:417)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init
    drm_core_init
    linker_stop_class_add
    linker_init_kernel_modules <-- Here
```

#### memguard\_sysinit (sys/vm/memguard.c:226)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init
    drm_core_init
    linker_stop_class_add
    linker_init_kernel_modules
    memguard_sysinit <-- Here
```

#### acpi\_pm\_register (sys/dev/acpica/acpi.c:4627)

```txt
Control Flow:
mi_startup
    ...
    ipoib_unrhdr_init
    ucom_init
    linker_init
    dpcpu_startup
    module_init
    vnet_data_startup
    usb_dev_init
    link_elf_init
    link_elf_init
    linker_preload
    drm_magic_init
    drm_core_init
    linker_stop_class_add
    linker_init_kernel_modules
    memguard_sysinit
    acpi_pm_register <-- Here
```

### SI\_SUB\_CPU

#### cpu\_startup (sys/amd64/amd64/machdep.c:223)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup <-- Here
```

#### cpu\_alloc (sys/x86/x86/mp\_x86.c:978)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc <-- Here
```

#### log\_msg (sys/x86/x86/ucode.c:84)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg <-- Here
```

#### psci\_init (sys/dev/psci/psci.c:136)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init <-- Here
```

#### apic\_setup\_local (sys/x86/x86/local\_apic.c:1904)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local <-- Here
```

#### mp\_start (sys/kern/subr\_smp.c:162)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start <-- Here
```

#### madt\_set\_ids (sys/x86/acpica/madt.c:754)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids <-- Here
```

#### cpu\_idle\_tun (sys/x86/x86/cpu\_machdep.c:810)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun <-- Here
```

#### x86bios\_modevent (sys/compat/x86bios/x86bios.c:842)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent <-- Here
```

#### cluster\_init (sys/kern/vfs\_cluster.c:81)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init <-- Here
```

#### boottrace\_init (sys/kern/kern\_boottrace.c:583)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init <-- Here
```

#### prng\_init (sys/kern/subr\_prng.c:72)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init <-- Here
```

#### callout\_callwheel\_init (sys/kern/kern\_timeout.c:275)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init <-- Here
```

#### fpuinitstate (sys/amd64/amd64/fpu.c:413)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate <-- Here
```

#### late\_ifunc\_resolve (sys/amd64/amd64/machdep.c:315)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve <-- Here
```

#### vnode\_pager\_init (sys/vm/vnode\_pager.c:137)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve
    vnode_pager_init <-- Here
```

#### mca\_init\_bsp (sys/x86/x86/mca.c:1496)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve
    vnode_pager_init
    mca_init_bsp <-- Here
```

#### x86\_mem\_drvinit (sys/x86/x86/x86\_mem.c:715)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve
    vnode_pager_init
    mca_init_bsp
    x86_mem_drvinit <-- Here
```

#### pmap\_delayed\_invl\_callout\_init (sys/amd64/amd64/pmap.c:1093)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve
    vnode_pager_init
    mca_init_bsp
    x86_mem_drvinit
    pmap_delayed_invl_callout_init <-- here
```

#### pmap\_cpu\_init (sys/amd64/amd64/pmap.c:11169)

```txt
Control Flow:
mi_startup
    ...
    cpu_startup
    cpu_alloc
    log_msg
    psci_init
    apic_setup_local
    mp_start
    madt_set_ids
    cpu_idle_tun
    x86bios_modevent
    cluster_init
    boottrace_init
    prng_init
    callout_callwheel_init
    fpuinitstate
    late_ifunc_resolve
    vnode_pager_init
    mca_init_bsp
    x86_mem_drvinit
    pmap_delayed_invl_callout_init
    pmap_cpu_init <-- Here
```

### SI\_SUB\_RACCT

#### racct\_init (sys/kern/kern\_racct.c:1350)

```txt
Control Flow:
mi_startup
    ...
    racct_init <-- Here
```

#### rctl\_init (sys/kern/kern\_rctl.c:2178)

```txt
Control Flow:
mi_startup
    ...
    racct_init
    rctl_init <-- Here
```

### SI\_SUB\_KDTRACE

#### stats\_init (sys/kern/subr\_stats.c:3694)

```txt
Control Flow:
mi_startup
    ...
    stats_init <-- Here
```

#### init\_hwpmc (sys/kern/kern\_pmc.c:336)

```txt
Control Flow:
mi_startup
    ...
    stats_init
    init_hwpmc <-- Here
```

#### dtrace\_debug\_init (sys/cddl/dev/dtrace/dtrace\_debug.c:65)

```txt
Control Flow:
mi_startup
    ...
    stats_init
    init_hwpmc
    dtrace_debug_init <-- Here
```

### SI\_SUB\_RANDOM

#### fxrng\_init\_alg (sys/dev/random/fenestrasX/fx\_main.c:277)

```txt
Control Flow:
mi_startup
    ...
    fxrng_init_alg <-- Here
```

#### random\_fortuna\_init\_alg (sys/dev/random/fortuna.c:277)

```txt
Control Flow:
mi_startup
    ...
    random_fortuna_init_alg <-- Here
```

#### random\_other\_init\_alg (sys/dev/random/other\_algorithm.c:115)

```txt
Control Flow:
mi_startup
    ...
    random_other_init_alg <-- Here
```

#### random\_alg\_context\_init (sys/dev/random/randomdev.c:92)

```txt
Control Flow:
mi_startup
    ...
    random_alg_context_init <-- Here
```

#### random\_harvestq\_init (sys/dev/random/random\_harvestq.c:428)

```txt
Control Flow:
mi_startup
    ...
    random_alg_context_init
    random_harvestq_init <-- Here
```

#### nehemiah\_modevent (sys/dev/random/nehemiah.c:95)

```txt
Control Flow:
mi_startup
    ...
    random_alg_context_init
    random_harvestq_init
    nehemiah_modevent <-- Here
```

#### darn\_modevent (sys/dev/random/darn.c:109)

```txt
Control Flow:
mi_startup
    ...
    random_alg_context_init
    random_harvestq_init
    nehemiah_modevent
    darn_modevent <-- Here
```

#### rndr\_modevent (sys/dev/random/armv8rng.c:93)

```txt
Control Flow:
mi_startup
    ...
    random_harvestq_init
    nehemiah_modevent
    darn_modevent
    rndr_modevent <-- Here
```

#### rdrand\_modevent (sys/dev/random/ivy.c:160)

```txt
Control Flow:
mi_startup
    ...
    nehemiah_modevent
    darn_modevent
    rndr_modevent
    rndrand_modevent <-- Here
```

#### random\_harvestq\_prime (sys/dev/random/random\_harvestq.c:498)

```txt
Control Flow:
mi_startup
    ...
    darn_modevent
    rndr_modevent
    rndrand_modevent
    random_harvestq_prime <-- Here
```

#### hashrandom\_init (sys/dev/mlx4/mlx4\_en\_tx.c:597)

```txt
Control Flow:
mi_startup
    ...
    rndr_modevent
    rndrand_modevent
    random_harvestq_prime
    hashrandom_init <-- Here
```

#### mlx5e\_hash\_init (sys/dev/mlx6/mlx6\_en/mlx5\_en\_tx.c:80)

```txt
Control Flow:
mi_startup
    ...
    rndrand_modevent
    random_harvestq_prime
    hashrandom_init
    mlx5e_hash_init <-- Here
```

#### \_\_stack\_chk\_init (sys/kern/stack\_protector.c:19)

```txt
Control Flow:
mi_startup
    ...
    random_harvestq_prime
    hashrandom_init
    mlx5e_hash_init
    __stack_chk_inti <-- Here
```

### SI\_SUB\_MAC

#### mac\_init (sys/security/mac/mac\_framework.c:318)

```txt
Control Flow:
mi_startup
    ...
    mac_init <-- Here
```

### SI\_SUB\_MAC\_POLICY

### SI\_SUB\_MAC\_LATE

#### mac\_late\_init (sys/security/mac/mac\_framework.c:338)

```txt
Control Flow:
mi_startup
    ...
    mac_late_init <-- Here

341: mac_late = 1;
```

#### mac\_veriexec\_late\_init (sys/security/mac\_veriexec/veriexec\_fingerprint.c:460)

```txt
Control Flow:
mi_startup
    ...
    mac_late_init
    mac_veriexec_late_init <-- Here

463: mac_veriexec_late = 1;
```

### SI\_SUB\_VNET

#### nfs\_vnetinit (sys/fs/nfs/nfs\_commonport.c:874)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit <-- Here
```

#### vnet\_init\_prelink (sys/net/vnet.c:310)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink <-- Here
```

#### vnet0\_init (sys/net/vnet.c:322)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init <-- Here
```

#### frag6\_slowtimo\_init (sys/netinet6/frag6.c:1004)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init <-- Here
```

#### svc\_rpc\_gss\_vnetinit (sys/rpc/rpcsec\_gss/svc\_rpcsec\_gss.c:223)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit <-- Here
```

#### rpctls\_vnetinit (sys/rpc/rpcsec\_tls/rpctls\_impl.c:99)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit
    rpctls_vnetinit <-- Here
```

#### fhanew\_init (sys/fs/nfsserver/nfs\_fha\_new.c:105)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    fhanew_init <-- Here
```

#### nfsrv\_vnetinit (sys/fs/nfsserver/nfs\_nfsdport.c:7176)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    fhanew_init
    nfsrv_vnetinit <-- Here
```

#### vnet\_init\_done (sys/net/vnet.c:338)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    fhanew_init
    nfsrv_vnetinit
    vnet_init_done <-- Here

341: curvnet = NULL;
```

#### vnet\_sysinit\_done (sys/net/vnet.c:364)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_prelink
    vnet0_init
    frag6_slowtimo_init
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    fhanew_init
    nfsrv_vnetinit
    vnet_init_done
    vnet_sysinit_done <-- Here

367: return;
```

### SI\_SUB\_INTRINSIC

#### f00f\_hack (sys/i386/i386/machdep.c:1807)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack <-- Here
```

#### proc0\_init (sys/kern/init\_main.c:463)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack
    proc0_init <-- Here
```

#### proc0\_post (sys/kern/init\_main.c:652)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack
    proc0_init
    proc0_post <-- Here
```

#### geom\_event\_init (sys/geom/geom\_event.c:108)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack
    proc0_init
    proc0_post
    geom_event_init <-- Here
```

#### fork\_init (sys/kern/kern\_fork.c:1238)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack
    proc0_init
    proc0_post
    geom_event_init
    fork_init <-- Here
```

#### shutdown\_conf (sys/kern/kern\_shutdown.c:262)

```txt
Control Flow:
mi_startup
    ...
    f00f_hack
    proc0_init
    proc0_post
    geom_event_init
    fork_init
    shutdown_conf <-- Here
```

### SI\_SUB\_VM\_CONF

#### vm\_stats\_init (sys/vm/vm\_meter.c:559)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init <-- Here
```

#### uma\_startup3 (sys/vm/uma\_core.c:3204)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3 <-- Here
```

#### max\_ldt\_segment (sys/amd64/amd64/sys\_machdep.c:82)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment <-- Here
```

#### ffs\_rawread\_setup (sys/ufs/ffs/ffs\_rawread.c:92)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment
    ffs_rawread_setup <-- Here
```

#### vm\_page\_init\_cache\_zones (sys/vm/vm\_page.c:211)

```txt
Control Flow:
mi_startup
    ...
    vm_stats_init
    uma_startup3
    max_ldt_segment
    ffs_rawread_setup
    vm_page_init_cache_zones <-- Here
```

### SI\_SUB\_DDB\_SERVICES

### SI\_SUB\_RUN\_QUEUE

### SI\_SUB\_KTRACE

### SI\_SUB\_OPENSOLARIS

### SI\_SUB\_AUDIT

### SI\_SUB\_CREATE\_INIT

#### create\_init (sys/kern/init\_main.c:815)

```txt
Control Flow:
mi_startup
    ...
    create_init <-- Here
```

### SI\_SUB\_SCHED\_IDLE

#### idle\_setup (sys/kern/kern\_idle.c:52)

```txt
Control Flow:
mi_startup
    ...
    idle_setup <-- Here
```

### SI\_SUB\_MBUF

#### mbuf\_init (sys/kern/kern\_mbuf.c:348)

```txt
Control Flow:
mi_startup
    ...
    mbuf_init <-- Here
```

#### sfstat\_init (sys/kern/kern\_sendfile.c:143)

```txt
Control Flow:
mi_startup
    ...
    mbuf_init
    sfstat_init <-- Here
```

#### sf\_buf\_init (sys/kern/subr\_sfbuf.c:83)

```txt
Control Flow:
mi_startup
    ...
    mbuf_init
    sfstat_init
    sf_buf_init <-- Here
```

### SI\_SUB\_INTR

#### intr\_irq\_init (sys/kern/subr\_intr.c:190)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init <-- Here
```

#### intr\_map\_init (sys/kern/subr\_intr.c:1759)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init <-- Here
```

#### xen\_hvm\_cpu\_init (sys/x86/xen/hvm.c:414)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init <--  Here
```

#### intr\_init (sysy/x86/x86/intr\_machdep.c:467)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init <-- Here
```

#### xen\_intr\_init (sys/dev/xen/bus/xen\_intr.c:445)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init <-- Here
```

#### apic\_setup\_io (sys/x86/x86/local\_apic.c:1926)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io <-- Here
```

#### atpic\_init (sys/x86/x86/intr\_machdep.c:504)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init <-- Here
```

#### intr\_init\_sources (sys/x86/x86/intr\_machdep.c:164)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init
    intr_init_sources <-- Here
```

#### xen\_intrcnt\_init (sys/x86/xen/xen\_arch\_intr.c:61)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init
    intr_init_sources
    xen_intrcnt_init <-- Here
```

#### mp\_ipi\_intrcnt (sys/x86/xen/xen\_arch\_intr.c:1706)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init
    intr_init_sources
    xen_intrcnt_init
    mp_ipi_intrcnt <-- Here
```

#### lapic\_intrcnt (sys/x86/x86/local\_apic.c:790)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init
    intr_init_sources
    xen_intrcnt_init
    mp_ipi_intrcnt
    lapic_intrcnt <-- Here
```

#### intr\_init\_final (sys/x86/x86/intr\_machdep.c:478)

```txt
Control Flow:
mi_startup
    ...
    intr_irq_init
    intr_map_init
    xen_hvm_cpu_init
    intr_init
    xen_intr_init
    apic_setup_io
    atpic_init
    intr_init_sources
    xen_intrcnt_init
    mp_ipi_intrcnt
    lapic_intrcnt
    intr_init_final <--  Here
```

### SI\_SUB\_TASKQ

#### vt\_init\_logos (sys/dev/vt/vt\_cpulogos.c:207)

```txt
Control Flow:
mi_startup
    ...
    vt_init_logos <-- Here
```

#### fxent\_pool\_timer\_init (sys/dev/random/fenestrasX/fx\_pool.c:601)

```txt
Control Flow:
mi_startup
    ...
    vt_init_logos
    fxent_pool_timer_init <-- Here
```

#### uma\_startup4 (sys/vm/uma\_core.c:3221)

```txt
Control Flow:
mi_startup
    ...
    vt_init_logos
    fxent_pool_timer_init
    uma_startup4 <-- Here
```

### SI\_SUB\_EPOCH

#### epoch\_init (sys/kern/subr\_epoch.c:300)

```txt
Control Flow:
mi_startup
    ...
    epoch_init <-- Here
```

#### rs\_epoch\_init (sys/dev/random/random\_harvestq.c:221)

```txt
Control Flow:
mi_startup
    ...
    epoch_init
    rs_epoch_init <-- Here
```

#### if\_epochalloc (sys/net/if.c:964)

```txt
Control Flow:
mi_startup
    ...
    epoch_init
    rs_epoch_init
    if_epochalloc <-- Here
```

### SI\_SUB\_SMP

#### invl\_scoreboard\_init (sys/amd64/adm64/mp\_machdep.c:526)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init <-- Here
```

#### release\_aps (sys/x86/x86/mp\_x86.c:1690)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps <-- Here
```

#### intr\_irq\_shuffle (sys/kern/subr\_intr.c:1262)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle <-- Here
```

#### kcsan\_enable (sys/kern/subr\_csan.c:87)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable <--  Here

90-91: printf("Enabling KCSCAN, expect reduced performance.\n");
       kcsan_enabled = true;
```

#### xen\_setup\_cpus (sys/x86/xen/xen\_apic.c:337)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus <-- Here
```

#### intr\_smp\_startup (sys/x86/x86/intr\_machdep.c:652)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup <-- Here
```

#### netisr\_start (sys/net/netisr.c:1353)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start <-- Here
```

#### kvm\_clock\_init\_smp (sys/dev/kvm\_clock/kvm\_clock.c:112)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp <-- Here
```

#### intel\_ntb\_msix\_ready (sys/dev/ntb/ntb\_hw/ntb\_hw\_intel.c:2981)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready <-- Here

2984: msix_ready = 1;
```

#### vmbus\_sysinit (sys/dev/hyperv/vmbus/vmbus.c:1698)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit <-- Here
```

#### lock\_prof\_init\_type (sys/kern/subr\_lock.c:284)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type <-- Here
```

#### dtrace\_debug\_init (sys/cddl/dev/dtrace/dtrace\_debug.c:65)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init <-- Here
```

#### dtrace\_ap\_start (sys/cddl/dev/dtrace/dtrace\_load.c:25)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start <-- Here
```

#### smp\_after\_idle\_runnable (sys/x86/x86/mp\_x86.c:1145)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable <-- Here
```

#### hw\_mds\_recalculate\_boot (sys/x86/x86/cpu\_machdep.c:1213)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot <-- Here
```

#### taa\_recalculate\_boot (sys/x86/x86/cpu\_machdep.c:1355)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot <-- Here
```

#### intr\_balance\_init (sys/x86/x86/intr\_machdep.c:772)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init <-- Here
```

#### init\_TSC\_tc (sys/x86/x86/tsc.c:653)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init
    init_TSC_tc <-- Here
```

#### epoch\_init\_smp (sys/kern/subr\_epoch.c:333)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init
    init_TSC_tc
    epoch_init_smp <-- Here

335: inited = 2;
```

#### tcp\_rs\_init (sys/netinet/tcp\_ratelimit.c:1773)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init
    init_TSC_tc
    epoch_init_smp
    tcp_rs_init <-- Here
```

#### vmm\_handler (sys/amd64/vmm/vmm.c:437)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init
    init_TSC_tc
    epoch_init_smp
    tcp_rs_init
    vmm_handler <-- Here
```

#### ucode\_release (sys/x86/x86/ucode.c:233)

```txt
Control Flow:
mi_startup
    ...
    invl_scoreboard_init
    release_aps
    intr_irq_shuffle
    kcsan_enable
    xen_setup_cpus
    intr_smp_startup
    netisr_start
    kvm_clock_init_smp
    intel_ntb_msix_ready
    vmbus_sysinit
    lock_prof_init_type
    dtrace_debug_init
    dtrace_ap_start
    smp_after_idle_runnable
    hw_mds_recalculate_boot
    taa_recalculate_boot
    intr_balance_init
    init_TSC_tc
    epoch_init_smp
    tcp_rs_init
    vmm_handler
    ucode_release <-- Here
```

### SI\_SUB\_SOFTINTR

#### netisr\_init (sys/net/netisr.c:1301)

```txt
Control Flow:
mi_startup
    ...
    netisr_init <-- Here
```

#### start\_softintr (sys/kern/kern\_intr.c:1601)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr <-- Here
```

#### start\_softclock (sys/kern/kern\_timeout.c:372)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr
    start_softclock <-- Here
```

#### rss\_init (sys/net/rss\_config.c:173)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr
    start_softclock
    rss_init <-- Here
```

#### init\_device\_poll (sys/kern/kern\_poll.c:270)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr
    start_softclock
    rss_init
    init_device_poll <-- Here
```

#### tcp\_hpts\_modevent (sys/netinet/tcp\_hpts.c:2068)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr
    start_softclock
    rss_init
    init_device_poll
    tcp_htps_modevent <-- Here
```

#### sysbeep\_init (sys/kern/kern\_cons.c:694)

```txt
Control Flow:
mi_startup
    ...
    netisr_init
    start_softintr
    start_softclock
    rss_init
    init_device_poll
    tcp_htps_modevent
    sysbeep_init <-- Here
```

### SI\_SUB\_DEVFS

#### cuse\_modevent (sys/fs/cuse/cuse.c:78)

```txt
Control Flow:
mi_startup
    ...
    cuse_modevent <-- Here
```

#### devfs\_devs\_init (sys/fs/devfs/devfs\_devs.c:745)

```txt
Control Flow:
mi_startup
    ...
    cuse_modevent
    devfs_devs_init <-- Here
```

#### reroot\_conf (sys/kern/kern\_shutdown.c:280)

```txt
Control Flow:
mi_startup
    ...
    cuse_modevent
    devfs_devs_init
    reroot_conf <-- Here
```

#### cuse\_kern\_init (sys/fs/cuse/cuse.c:296)

```txt
Control Flow:
mi_startup
    ...
    cuse_modevent
    devfs_devs_init
    reroot_conf
    cuse_kern_init <-- Here
```

### SI\_SUB\_INIT\_IF

#### hhook\_vnet\_init (sys/kern/kern\_hhook.c:481)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init <-- Here
```

#### if\_init\_idxtable (sys/net/if.c:424)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable <-- Here
```

#### vnet\_if\_init (sys/net/if.c:433)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init <-- Here
```

#### xz\_module\_event\_handler (sys/dev/xz/xz\_mod.c:56)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init
    xz_module_event_handler <-- Here
```

#### ether\_init (sys/net/if\_ethersubr.c:766)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init
    xz_module_event_handler
    ether_init <-- Here
```

#### iflib\_module\_event\_handler (sys/net/iflib.c:5670)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init
    xz_module_event_handler
    ether_init
    iflib_module_event_handler <-- Here
```

#### infiniband\_modevent (sys/net/if\_infiniband.c:668)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init
    xz_module_event_handler
    ether_init
    iflib_module_event_handler
    infiniband_modevent <-- Here
```

#### firewire\_modevent (sys/net/if\_fwsubr.c:847)

```txt
Control Flow:
mi_startup
    ...
    hhook_vnet_init
    if_init_idxtable
    vnet_if_init
    xz_module_event_handler
    ether_init
    iflib_module_event_handler
    infiniband_modevent <-- Here
```

### SI\_SUB\_NETGRAPH

### SI\_SUB\_DTRACE

### SI\_SUB\_DTRACE\_PROVIDER

### SI\_SUB\_DTRACE\_ANON

### SI\_SUB\_DRIVERS

### SI\_SUB\_CONFIGURE

### SI\_SUB\_VFS

#### acl\_nfs4\_modload (sys/kern/subr\_acl\_nfs4.c:1372)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload <-- Here
```

#### vntblinit (sys/kern/vfs\_subr.c:716)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit <-- Here
```

#### acl\_posix1e\_modload (sys/kern/subr\_acl\_posix1e.c:642)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload <-- Here
```

#### nfscl\_modevent (sys/fs/nfsclient/nfs\_clport.c:1425)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent <-- Here
```

#### nchinit (sys/kern/vfs\_cache.c:2669)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit <-- Here
```

#### nameiinit (sys/kern/vfs\_lookup.c:175)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit <-- Here
```

#### vfs\_hashinit (sys/kern/vfs\_hash.c:47)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit <-- Here
```

#### mq\_modload (sys/kern/uipc\_mqueue.c:2909)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload <-- Here
```

#### fuse\_loader (sys/fs/fuse/fuse\_main.c:134)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader <-- Here
```

#### aio\_modload (sys/kern/vfs\_aio.c:371)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload <-- Here
```

#### soaio\_init (sys/kern/sys\_socket.c:574)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init <-- Here
```

#### pipeinit (sys/kern/sys\_pipe.c:257)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit <-- Here
```

#### vfs\_mount\_init (sys/kern/vfs\_mount.c:181)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init <-- Here
```

#### vfs\_event\_init (sys/kern/vfs\_subr.c:6394)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init <-- Here
```

#### timerfd\_init (sys/kern/sys\_timerfd.c:105)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init <-- Here
```

#### svc\_rpc\_gss\_init (sys/rpc/rpcsec\_gss/svc\_rpcsec\_gss.c:204)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init <-- Here
```

#### krpc\_modevent (sys/rpc/rpc\_generic.c:960)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent <-- Here
```

#### kgssapi\_modevent (sys/kgssapi/gss\_impl.c:312)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent <-- Here
```

#### kgssapi\_krb5\_modevent (sys/kgssapi/krb5/k4b5\_mech.c:2100)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent <-- Here
```

#### nfslockd\_modevent (sys/nlm/nlm\_prot\_impl.c:2384)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent
    nfslockd_modevent <-- Here
```

#### nfssvc\_modevent (sys/nfs/nfs\_nfssvc.c:119)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent
    nfslockd_modevent
    nfssvc_modevent <-- Here
```

#### xdr\_modevent (sys/xdr/xdr.c:818)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent
    nfslockd_modevent
    nfssvc_modevent
    xdr_modevent <-- Here

821: return (0);
```

#### nfsd\_modevent (sys/fs/nfsserver/nfs\_nfsdport.c:7245)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent
    nfslockd_modevent
    nfssvc_modevent
    xdr_modevent
    nfsd_modevent <-- Here
```

#### nfscommon\_modevent (sys/fs/nfs/nfs\_commonport.c:909)

```txt
Control Flow:
mi_startup
    ...
    acl_nfs4_modload
    vntblinit
    acl_posix1e_modload
    nfscl_modevent
    nchinit
    nameiinit
    vfs_hashinit
    mq_modload
    fuse_loader
    aio_modload
    soaio_init
    pipeinit
    vfs_mount_init
    vfs_event_init
    timerfd_init
    svc_rpc_gss_init
    krpc_modevent
    kgssapi_modevent
    kgssapi_krb5_modevent
    nfslockd_modevent
    nfssvc_modevent
    xdr_modevent
    nfsd_modevent
    nfscommon_modevent <-- Here
```

### SI\_SUB\_CLOCKS

#### initclocks (sys/kernkern\_clock.c:418)

```txt
Control Flow:
mi_startup
    ...
    initclocks <-- Here
```

#### inittimecounter (sys/kern/kern\_tc.c:1997)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter <-- Here
```

#### sched\_initticks (sys/kern/sched\_4bsd.c:650)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter
    sched_initticks <-- Here (4BSD)
```

#### sched\_initticks (sys/kern/sched\_ule.c:1556)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter
    sched_initticks <-- Here (ULE)
```

#### e1000\_enable\_pause\_delay (sys/dev/e1000/e1000\_osdep.c:40)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter
    sched_initticks (ULE)
    e1000_enable_pause_delay <-- Here
```

#### zfs\_modevent (sys/contrib/openzfs/module/os/freebsd/zfs/kmod\_core.c:303)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter
    sched_initticks (ULE)
    e1000_enable_pause_delay
    zfs_modevent <-- Here
```

#### deadlkres (sys/kern/kern\_clock.c:240)

```txt
Control Flow:
mi_startup
    ...
    initclocks
    inittimecounter
    sched_initticks (ULE)
    e1000_enable_pause_delay
    zfs_modevent
    deadlkres <-- Here (kthread_start)
```

### SI\_SUB\_PSEUDO

### SI\_SUB\_EXEC

#### sysinit\_register\_elf64\_brand\_entries (sys/amd64/amd64/elf\_machdep.c:205)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries <-- Here
```

#### shared\_page\_init (sys/kern/kern\_sharedpage.c:115)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init <-- Here
```

#### pfs\_modevent (sys/fs/pseudofs/pseudofs.c:487)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent <-- Here
```

#### imgact\_binmisc\_init (sys/kern/imgact\_binmisc.c:747)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init <-- Here
```

#### cxgbei\_modevent (sys/dev/cxgbe/cxgbei/cxgbei.c:943)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init <-- Here
```

#### mod\_event (sys/dev/cxgbe/if\_ccv.c:34)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event <-- Here

37: return (0);
```

#### mod\_event (sys/dev/cxgbe/if\_cc.c:34)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event <-- Here

37: return (0);
```

#### mod\_event (sys/dev/cxgbe/if\_cxl.c:34)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event <-- Here

37: return (0);
```

#### mod\_event (sys/dev/cxgbe/if\_cxlv.c:34)

```txt
Control Flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event <-- Here

37: return (0);
```

#### c4iw\_modevent (sys/dev/cxgbe/iw\_cxgbe/device.c:429)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent <-- here
```

#### t4\_tom\_modevent (sys/dev/cxgbe/tom/t4\_tom.c:2295)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent <-- Here
```

#### toecore\_mod\_handler (sys/netinet/toecore.c:585)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler <-- Here
```

#### ia32\_syscall\_enable (sys/amd64/ia32/ia32\_syscall.c:249)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable <-- Here
```

#### amd64\_init\_sysvecs (sys/amd64/amd64/elf\_machdep.c:144)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs <-- Here
```

#### i386\_setup\_lcall\_gate (sys/i386/i386/machdep.c:1702)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs
    i386_setup_lcall_gate <-- Here
```

#### aout\_sysent (sys/kern/imgact\_aout.c:155)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs
    i386_setup_lcall_gate
    aout_sysent <-- Here
```

#### exec\_prealloc\_args\_kva (sys/kern/kern\_exec.c:1402)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs
    i386_setup_lcall_gate
    aout_sysent
    exec_prealloc_args_kva <-- Here
```

#### register\_compat32\_feature (sys/compat/freebsd32/freebsd32\_misc.c:129)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs
    i386_setup_lcall_gate
    aout_sysent
    exec_prealloc_args_kva
    register_compat32_feature <-- Here
```

#### fxrng\_vdso\_sysinit (sys/dev/random/fenestrasX/fx\_brng.c:145)

```txt
control flow:
mi_startup
    ...
    sysinit_register_elf64_brand_entries
    shared_page_init
    pfs_modevent
    imgact_binmisc_init
    mod_event
    mod_event
    mod_event
    mod_event
    c4iw_modevent
    t4_tom_modevent
    toecore_mod_handler
    ia32_syscall_enable
    amd64_init_sysvecs
    i386_setup_lcall_gate
    aout_sysent
    exec_prealloc_args_kva
    register_compat32_feature
    fxrng_vdso_sysinit <-- Here
```

### SI\_SUB\_PROTO\_BEGIN

#### cdg\_init\_vnet (sys/netinet/cc/cc\_cdg.c:245)

```txt
Control Flow:
mi_startup
    ...
    cdg_init_vnet <-- Here
```

### SI\_SUB\_PROTO\_PFIL

#### pfil\_init (sys/net/pfil.c:526)

```txt
Control Flow:
mi_startup
    ...
    pfil_init <-- Here
```

### SI\_SUB\_IF

Nothing here surprisingly 

### SI\_SUB\_DOMAININIT

Nothing here surprisingly 

### SI\_SUB\_MC

Nothing here surprisingly 

### SI\_SUB\_DOMAIN

Nothing here surprisingly 

### SI\_SUB\_FIREWALL

#### ipfw\_modevent (sys/netpfil/ipfw/ip\_fw2.c:3644)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent <-- Here
```

#### ipfw\_init (sys/netpfil/ipfw/ip\_fw2.c:3438)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent
    ipfw_init <-- Here
```

#### vnet\_ipfw\_init (sys/netpfil/ipfw/ip\_fw2.c:3507)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent
    ipfw_init
    vnet_ipfw_init <-- Here
```

#### ipfw\_nat\_modevent (sys/netpfil/ipfw/ip\_fw\_nat.c:1202)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent
    ipfw_init
    vnet_ipfw_init
    ipfw_nat_modevent <-- Here
```

#### ipfw\_nat\_init (sys/netpfil/ipfw/ip\_fw\_nat.c:1170)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent
    ipfw_init
    vnet_ipfw_init
    ipfw_nat_modevent
    ipfw_nat_init <-- Here
```

#### vnet\_ipfw\_nat\_init (sys/netpfil/ipfw/ip\_fw\_nat.c:1144)

```txt
Control Flow:
mi_startup
    ...
    ipfw_modevent
    ipfw_init
    vnet_ipfw_init
    ipfw_nat_modevent
    ipfw_nat_init
    vnet_ipfw_nat_init <-- Here

1147: V_ipfw_nat_ready = 1;

1148: return (0);
```

### SI\_SUB\_IFATTACHDOMAIN

#### ipfw\_pmod\_modevent (sys/netpfil/ipfw/pmod/ip\_fw\_pmod.c:66)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent <-- Here
```

#### vnet\_ipfw\_pmod\_init (sys/netpfil/ipfw/pmod/ip\_fw\_pmod.c:49)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent
    vnet_ipfw_pmod_init <-- Here
```

#### ipfw\_nptv6\_modevent (sys/netpfil/ipfw/nptv6/ip\_fw\_nptv6.c:64)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent
    vnet_ipfw_pmod_init
    ipfw_nptv6_modevent <-- Here
```

#### vnet\_ipfw\_nptv6\_init (sys/netpfil/ipfw/nptv6/ip\_fw\_nptv6.c:49)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent
    vnet_ipfw_pmod_init
    ipfw_nptv6_modevent
    vnet_ipfw_nptv6_init <-- Here
```

#### ipfw\_nat64\_modevent (sys/netpfil/ipfw/nat64/ip\_fw\_nat64.c:119)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent
    vnet_ipfw_pmod_init
    ipfw_nptv6_modevent
    vnet_ipfw_nptv6_init
    ipfw_nat64_modevent <-- Here
```

#### vnet\_ipfw\_nat64\_init (sys/netpfil/ipfw/nat64/ip\_fw\_nat64.c:78)

```txt
Control Flow:
mi_startup
    ...
    ipfw_pmod_modevent
    vnet_ipfw_pmod_init
    ipfw_nptv6_modevent
    vnet_ipfw_nptv6_init
    ipfw_nat64_modevent
    vnet_ipfw_nat64_init <-- Here
```

### SI\_SUB\_PROTO\_END

Nothing here surprisingly 

### SI\_SUB\_KICK\_SCHEDULER

#### usb\_dev\_init\_post (sys/dev/usb/usb\_dev.c:977)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post <-- Here
```

#### sync\_setup (sys/kern/kern\_sync.c:655)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup <-- Here
```

#### ena\_rss\_init\_default\_deferred (sys/dev/ena/ena\_rss.c:197)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred <-- Here
```

#### usb\_needs\_explore\_init (sys/dev/usb/usb\_hub.c:2349)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred
    usb_needs_explore_init <-- Here
```

#### random\_kthread (sys/dev/random/random\_harvsetq.c:180)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred
    usb_needs_explore_init
    random_kthread <-- Here (krpoc_start)
```

#### acpi\_taskq\_init (sys/dev/acpica/Osd/OsdSchedule.c:109)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred
    usb_needs_explore_init
    random_kthread
    acpi_taskq_init <-- Here
```

#### acpi\_tz\_startup (sys/dev/acpica/acpi\_thermal.c:331)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred
    usb_needs_explore_init
    random_kthread
    acpi_taskq_init
    acpi_tz_startup <-- Here
```

#### mca\_startup (sys/x86/x86/mca.c:1067)

```txt
Control Flow:
mi_startup
    ...
    usb_dev_init_post
    sync_setup
    ena_rss_init_default_deferred
    usb_needs_explore_init
    random_kthread
    acpi_taskq_init
    acpi_tz_startup
    mca_startup <-- Here
```

### SI\_SUB\_INIT\_CONFIG\_HOOKS

Nothing here surprisingly

### SI\_SUB\_ROOT\_CONF

#### nfs\_rootconf (sys/nfs/nfs\_diskless.c:433)

```txt
Control Flow:
mi_startup
    ...
    nfs_rootconf <-- Here
```

#### bootpc\_init (sys/nfs/bootp\_subr.c:1512)

```txt
Control Flow:
mi_startup
    ...
    bootpc_init <-- Here
```

### SI\_SUB\_INTRINSIC\_POST

#### proc0\_post (sys/kern/init\_main.c:652)

```txt
Control Flow:
mi_startup
    ...
    proc0_post <-- Here
```

### SI\_SUB\_SYSCALLS

#### selectinit (sys/kern/sys\_generic.c:2062)

```txt
Control Flow:
mi_startup
    ...
    selectinit <-- Here
```

#### sctp\_syscalls\_init (sys/netinet/sctp\_syscalls.c:101)

```txt
Control Flow:
mi_startup
    ...
    selectinit
    sctp_syscalls_init <-- Here
```

### SI\_SUB\_VNET\_DONE

#### nfs\_vnetinit (sys/fs/nfs/nfs\_commonport.c:874)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit <-- Here
```

#### vnet\_init\_done (sys/net/vnet.c:338)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done <-- Here
```

#### vnet\_sysinit\_done (sys/net/vnet.c:364)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done <-- Here
```

#### svc\_rpc\_gss\_vnetinit (sys/rpc/rpcsec\_gss/sbc\_rpcsec\_gss.c:223)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit <-- Here
```

#### rpctls\_vnetinit (sys/rpc/rpcsec\_tls/rpctls\_impl.c:99)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit
    rpctls_vnetinit <-- Here
```

#### frag6\_slowtimo\_init (sys/netinet6/frag6.c:1004)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    frag6_slowtimo_init <-- Here
```

#### fhanew\_init (sys/fs/nfsserver/nfs\_fha\_new.c:105)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    frag6_slowtimo_init
    fhanew_init <-- Here
```

#### nfsrv\_vnetinit (sys/fs/nfsserver/nfs\_nfsdport.c:7176)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    frag6_slowtimo_init
    fhanew_init
    nfsrv_vnetinit <-- Here

7179: Calls nfsd_mntinit.
```

#### nfsd\_mntinit (sys/fs/nfsserver/nfs\_nfsdport.c:3600)

```txt
Control Flow:
mi_startup
    ...
    nfs_vnetinit
    vnet_init_done
    vnet_sysinit_done
    svc_rpc_gss_vnetinit
    rpctls_vnetinit
    frag6_slowtimo_init
    fhanew_init
    nfsrv_vnetinit
    nfsd_mntinit <-- Here
```

### SI\_SUB\_KTHREAD\_INIT

#### linker\_preload\_finish (sys/kern/kern\_linker.c:1784)

```txt
Control Flow:
mi_startup
    ...
    linker_preload_finish <-- Here
```

#### kick\_init (sys/kern/init\_main.c:860)

```txt
Control Flow:
mi_startup
    ...
    linker_preload_finish
    kick_init <-- Here
```

### SI\_SUB\_KTHREAD\_PAGE

#### vm\_pageout\_init (sys/vm/vm\_pageout.c:2301)

```txt
Control Flow:
mi_startup
    ...
    vm_pageout_init <-- Here
```

#### kproc\_start (sys/vm/kern\_kthread.c:60)

```txt
Control Flow:
mi_startup
    ...
    vm_pageout_init
    kproc_start <-- Here

Note: Called with page_kp as an argument.
```

#### vm\_pageout (sys/vm/vm\_pageout.c:2349)

```txt
Control Flow:
mi_startup
    ...
    vm_pageout_init
    kproc_start --> vm_pageout <-- Here
```

### SI\_SUB\_KTHREAD\_VM

#### vm\_daemon (sys/vm/vm\_swapout.c:371)

```txt
Control Flow:
mi_startup
    ...
    kproc_start --> vm_daemon <-- Here
```

#### poll\_idle (sys/kern/kern\_poll.c:552)

```txt
Control Flow:
mi_startup
    ...
    kproc_start
    kproc_start --> poll_idle <-- Here
```

### SI\_SUB\_KTHREAD\_BUF

#### buf\_daemon (sys/kern/vfs\_bio.c:3447)

```txt
Control Flow:
mi_startup
    ...
    kproc_start --> buf_daemon <-- Here
```

#### pbuf\_prealloc (sys/vm/vm\_pager.c:241)

```txt
Control Flow:
mi_startup
    ...
    buf_daemon
    pbuf_prealloc <-- Here
```

### SI\_SUB\_KTHREAD\_UPDATE

#### vnlru\_proc (sys/kern/vfs\_subr.c:1740)

```txt
Control Flow:
mi_startup
    ...
    kproc_start --> vnlru_proc <-- Here
```

#### sched\_sync (sys/kern/vfs\_subr.c:2951)

```txt
Control Flow:
mi_startup
    ...
    vnlru_proc
    kproc_start --> sched_sync <-- Here
```

### SI\_SUB\_IDLE

Nothing here surprisingly

### SI\_SUB\_RACCTD

#### racctd\_init (sys/kern/kern\_ract.c:1340)

```txt
Control Flow:
mi_startup
    ...
    racctd_init <-- Here
```

### SI\_SUB\_LAST

