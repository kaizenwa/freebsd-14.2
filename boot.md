## Walkthrough of FreeBSD 14.2's Boot Code

#### btext (sys/amd64/amd64/locore.S:63)

```txt
Control Flow:
btext <-- Here
```
```asm
/**********************************************************************
 *
 * This is where the loader trampoline start us, set the ball rolling...
 *
 * We are called with the stack looking like this:
 * 0(%rsp) = 32 bit return address (cannot be used)
 * 4(%rsp) = 32 bit modulep
 * 8(%rsp) = 32 bit kernend
 *
 * We are already in long mode, on a 64 bit %cs and running at KERNBASE.
 */
ENTRY(btext)

	/* Don't trust what the loader gives for rflags. */
	pushq	$PSL_KERNEL
	popfq

	/* Get onto a stack that we can trust - there is no going back now. */
	movq	%rsp, %rbp
	movq	$bootstack,%rsp

#ifdef KASAN
	/* Bootstrap a shadow map for the boot stack. */
	movq	$bootstack, %rdi
	subq	$BOOTSTACK_SIZE, %rdi
	movq	$BOOTSTACK_SIZE, %rsi
	call	kasan_init_early
#endif

	/* Grab metadata pointers from the loader. */
	movl	4(%rbp),%edi		/* modulep (arg 1) */
	movl	8(%rbp),%esi		/* kernend (arg 2) */
	xorq	%rbp, %rbp

	call	hammer_time		/* set up cpu for unix operation */
	movq	%rax,%rsp		/* set up kstack for mi_startup() */
	call	mi_startup		/* autoconfiguration, mountroot etc */
0:	hlt
	jmp	0b
```

#### kasan\_early\_init (sys/kern/subr\_asan.c:152)

```txt
Control Flow:
btext
    kasan_early_init <-- Here

148: Calls kasan_md_init_early.
```

#### kasan\_md\_init\_early (sys/adm64/cinclude/asan.h:70)

```txt
Control Flow:
btext
    kasan_early_init
        kasan_md_init_early <-- Here

72: kasan_shadow_map(bootstack, size);
```

#### kasan\_shadow\_map (sys/kern/subr\_asan.c:103)

```txt
Control Flow:
btext
    kasan_early_init
        kasan_md_init_early
            kasan_shadow_map <-- Here
```

#### hammer\_time (sys/amd64/amd64/machdep.c:1288)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time <-- Here

1299: Calls TSRAW.

1301: Calls amd64_loadaddr.

1305: Calls native_parse_preload_data.

1307: Calls preload_search_info.

1315: Calls ucode_load_bsp.

1316: Calls roundup2.

1318: Calls identify_cpu1.

1319: Calls identify_hypervisor.

1320: Calls identify_hypervisor_smbios.

1321: Calls identify_cpu_fixup_bsp.

1322: Calls identify_cpu2.

1323: Calls initializecpucache.

1330: Calls pti_get_default.

1331: Calls TUNABLE_INT_FETCH on "vm.pmap.pti".

1332: Calls TUNABLE_INT_FETCH on "vm.pmap.pcid_enabled".

1344-1345: Calls TUNABLE_INT_FETCH on "vmo.pmap.pcid_invlpg_workaround".

1346: Calls cpu_init_small_core.

1353: Calls link_elf_ireloc.

1359: Calls proc_linkup0.

1362: Calls init_param1.

1375: Calls pmap_thread_init_invl_gen.

1378: Calls pcpu_init.

1390: Calls ssdtosyssd.

1395: Calls lgdt.

1397: Calls wrmsr on MSR_FSBASE.

1398: Calls wrmsr on MSR_GSBASE.

1399: Calls wrmsr on MSR_KGSBASE.

1401: Calls dpcpu_init.

1403: Calls amd64_bsp_pcpu_init1.

1414: Calls mutex_init.

1415: Calls mtx_init on icu_lock.

1416: Calls mtx_init on dt_lock.

1418-1462: Calls setidt to initialize the IDT.

1466: Calls lidt.

1487: Calls zenbleed_sanitize_enable.

1489: Calls finishidentcpu.

1501: Calls clock_init.

1503: Calls initializecpu.

1505: Calls amd64_bsp_ist_init.

1512: Calls ltr.

1514: Calls amd64_conf_fast_syscall.

1534: Calls cninit.

1535: Calls amd64_kdb_init.

1538: Calls getmemsize.

1539: Calls init_param2.

1545: Calls pci_early_quirks.

1557: Calls preload_dump.

1561: Calls elcr_probe.

1562: Calls atpic_startup.

1581: Calls msgbufinit.

1582: Calls fpuinit.

1589: Calls amd64_bsp_pcpu_init2.

1599: Calls load_ds.

1560: Calls load_es.

1601: Calls load_fs.

1610: Calls kcsan_cpu_init.

1613: Calls x86_init_fdt.

1617: Calls kasan_init.

1618: Calls kmsan_init.

1620: Calls TSEXIT.

1623: return (thread0.td_md.md_stack_base);
```

#### TSRAW (stand/libsa/stand.h:545)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        TSRAW <-- Here

545: #define TSRAW(a, b, c) tslog(a, b, c)
```

#### native\_parse\_preload\_data (sys/amd64/amd64/machdep.c:1131)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        TSRAW
        native_parse_preload_data <-- Here
```

#### preload\_search\_info (sys/kern/subr\_module.c:162)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        TSRAW
        native_parse_preload_data
        preload_search_info <-- Here
```

#### ucode\_load\_bsp (sys/x86/x86/ucode.c:315)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        TSRAW
        native_parse_preload_data
        preload_search_info
        ucode_load_bsp <-- Here
```

#### roundup2 (sys/sys/param.h:327)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        native_parse_preload_data
        preload_search_info
        ucode_load_bsp
        roundup2 <-- Here
```

#### identify\_cpu1 (sys/x86/x86/identcpu.c:1515)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        preload_search_info
        ucode_load_bsp
        roundup2
        identify_cpu1 <-- Here
```

#### identify\_hypervisor (sys/x86/x86/identcpu.c:1432)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        ucode_load_bsp
        roundup2
        identify_cpu1
        identify_hypervisor <-- Here
```

#### identify\_hypervisor\_smbios (sys/dev/smbios/smbios\_subr.c:67)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        roundup2
        identify_cpu1
        identify_hypervisor
        identify_hypervisor_smbios <-- Here
```

#### identify\_cpu\_fixup\_bsp (sys/x86/x86/identcpu.c:1581)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        identify_cpu1
        identify_hypervisor
        identify_hypervisor_smbios
        identify_cpu_fixup_bsp <-- Here
```

#### identify\_cpu2 (sys/x86/x86/identcpu.c:1534)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        identify_hypervisor
        identify_hypervisor_smbios
        identify_cpu_fixup_bsp
        identify_cpu2 <-- Here
```

#### initializecpucache (sys/amd64/amd64/initcpu.c:352)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        identify_hypervisor_smbios
        identify_cpu_fixup_bsp
        identify_cpu2
        initializecpucache <-- Here
```

#### pti\_get\_default (sys/x86/x86/identcpu.c:1748)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        identify_cpu_fixup_bsp
        identify_cpu2
        initializecpucache
        pti_get_default <-- Here
```

#### TUNABLE\_INT\_FETCH (sys/sys/kernel.h:333)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        identify_cpu2
        initializecpucache
        pti_get_default
        TUNABLE_INT_FETCH <-- Here
```

#### cpu\_init\_small\_core (sys/amd64/amd64/initcpu.c:253)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        initializecpucache
        pti_get_default
        TUNABLE_INT_FETCH
        cpu_init_small_core <-- Here
```

#### link\_elf\_ireloc (sys/kern/link\_elf.c:1962)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        pti_get_default
        TUNABLE_INT_FETCH
        cpu_init_small_core
        link_elf_ireloc <-- Here
```

#### proc0\_linkup (sys/kern/kern\_thread.c:503)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        TUNABLE_INT_FETCH
        cpu_init_small_core
        link_elf_ireloc
        proc0_linkup <-- Here
```

#### init\_param1 (sys/kern/subr\_param.c:170)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        cpu_init_small_core
        link_elf_ireloc
        proc0_linkup
        init_param1 <-- Here
```

#### pmap\_thread\_init\_invl\_gen ()

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        link_elf_ireloc
        proc0_linkup
        init_param1
        pmap_thread_init_invl_gen <-- Here
```

#### pcpu\_init (sys/kern/subr\_pcpu.c:84)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        proc0_linkup
        init_param1
        pmap_thread_init_invl_gen
        pcpu_init <-- Here
```

#### ssdtosyssd (sys/amd64/amd64/machdep.c:616)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        init_param1
        pmap_thread_init_invl_gen
        pcpu_init
        ssdtosyssd <-- Here
```

#### lgdt (sys/amd64/amd64/support.S:1472)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        pmap_thread_init_invl_gen
        pcpu_init
        ssdtosyssd
        lgdt <-- Here
```

#### wrmsr (sys/amd64/include/cpufunc.h:380)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        pcpu_init
        ssdtosyssd
        lgdt
        wrmsr <-- Here
```

#### dpcpu\_init (sys/kern/subr\_pcpu.c:100)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        ssdtosyssd
        lgdt
        wrmsr
        dpcpu_init <-- Here
```

#### amd64\_bsp\_pcpu\_init1 (sys/amd64/amd64/machdep.c:1194)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        lgdt
        wrmsr
        dpcpu_init
        amd64_bsp_pcpu_init1 <-- Here
```

#### mutex\_init (lib/libc/include/reetrant.h:97)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        wrmsr
        dpcpu_init
        amd64_bsp_pcpu_init1
        mutex_init <-- Here
```

#### mtx\_init (sys/sys/mutex.h:168)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        dpcpu_init
        amd64_bsp_pcpu_init1
        mutex_init
        mtx_init <-- Here

168-169: #define mtx_init(m, n, t, o)                       \
             _mtx_init(&(m)->mtx_lock, n, t, o)
```

#### setidt (sys/amd64/amd64/machdep.c:480)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        amd64_bsp_pcpu_init1
        mutex_init
        mtx_init
        setidt <-- Here
```

#### lidt (sys/amd64/include/cpufunc.h:712)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        mutex_init
        mtx_init
        setidt
        lidt <-- Here
```

#### zenbleed\_sanitize\_enable (sys/x86/x86/cpu\_machdep.c:1517)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        mtx_init
        setidt
        lidt
        zenbleed_sanitize_enable <-- Here
```

#### finishidentcpu (sys/x86/x86/identcpu.c:1597)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        setidt
        lidt
        zenbleed_sanitize_enable
        finishidentcpu <-- Here
```

#### clock\_init (sys/x86/isa/clock.c:129)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        lidt
        zenbleed_sanitize_enable
        finishidentcpu
        clock_init <-- Here
```

#### initializecpu (sys/amd64/amd64/initcpu.c:276)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        zenbleed_sanitize_enable
        finishidentcpu
        clock_init
        initializecpu <-- Here
```

#### amd64\_bsp\_ist\_init (sys/amd64/amd64/machdep.c:1221)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        finishidentcpu
        clock_init
        initializecpu
        amd64_bsp_ist_init <-- Here
```

#### GSEL (sys/x86/include/segments.h:56)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        clock_init
        initializecpu
        amd64_bsp_ist_init
        GSEL <-- Here

56: #define GSEL(s,r) (((s)<<3) | r)    /* a global selector */
```

#### ltr (sys/amd64/include/cpufunc.h:742)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        initializecpu
        amd64_bsp_ist_init
        GSEL
        ltr <-- Here
```

#### amd64\_conf\_fast\_syscall (sys/amd64/amd64/machdep.c:1178)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        amd64_bsp_ist_init
        GSEL
        ltr
        amd64_conf_fast_syscall <-- Here
```

#### set\_top\_of\_stack\_td (sys/amd64/vm\_machdep.c:88)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        GSEL
        ltr
        amd64_conf_fast_syscall
        set_top_of_stack_td <-- Here
```

#### cninit (sys/kern/kern\_cons.c:132)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        ltr
        amd64_conf_fast_syscall
        set_top_of_stack_td
        cninit <-- Here
```

#### amd64\_kdb\_init (sys/amd64/amd64/machdep.c:1167)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        amd64_conf_fast_syscall
        set_top_of_stack_td
        cninit
        amd64_kdb_init <-- Here
```

#### getmemsize (sys/amd64/amd64/machdep.c:862)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        set_top_of_stack_td
        cninit
        amd64_kdb_init
        getmemsize <-- Here
```

#### init\_param2 (sys/kern/subr\_param.c:259)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        cninit
        amd64_kdb_init
        getmemsize
        init_param2 <-- Here
```

#### pci\_early\_quirks (sys/x86/pci/pci\_early\_quirks.c:319)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        amd64_kdb_init
        getmemsize
        init_param2
        pci_early_quirks <-- Here
```

#### preload\_dump (sys/kern/subr\_module.c:545)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        getmemsize
        init_param2
        pci_early_quirks
        preload_dump <-- Here
```

#### elcr\_probe (sys/x86/isa/elcr.c:63)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        init_param2
        pci_early_quirks
        preload_dump
        elcr_probe <-- Here
```

#### atpic\_startup (sys/x86/isa/atpic.c:451)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        pci_early_quirks
        preload_dump
        elcr_probe
        atpic_startup <-- Here
```

#### atpic\_reset (sys/x86/x86/intr\_machdep.c:495)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        preload_dump
        elcr_probe
        atpic_startup
        atpic_reset <-- Here
```

#### msgbufinit (sys/kern/subr\_prf.c:1033)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        elcr_probe
        atpic_startup
        atpic_reset
        msgbufinit <-- Here
```

#### fpuinit (sys/amd64/amd64/fpu.c:355)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        atpic_startup
        atpic_reset
        msgbufinit
        fpuinit <-- Here
```

#### amd64\_bsp\_pcpu\_init2 (sys/amd64/amd64/machdep.c:1211)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        atpic_reset
        msgbufinit
        fpuinit
        amd64_bsp_pcpu_init2 <-- Here
```

#### load\_ds (sys/amd64/include/cpufunc.h:580)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        msgbufinit
        fpuinit
        amd64_bsp_pcpu_init2
        load_ds <-- Here
```

#### load\_es (sys/amd64/include/cpufunc.h:586)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        fpuinit
        amd64_bsp_pcpu_init2
        load_ds
        load_es <-- Here
```

#### load\_fs (sys/amd64/include/cpufunc.h:628)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        amd64_bsp_pcpu_init2
        load_ds
        load_es
        load_fs <-- Here
```

#### kcsan\_cpu\_init (sys/kern/subr\_casn.c:96)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        load_ds
        load_es
        load_fs
        kcsan_cpu_init <-- Here
```

#### x86\_init\_fdt (sys/x86/x86/fdt\_machdep.c:44)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        load_es
        load_fs
        kcsan_cpu_init
        x86_init_fdt <-- Here
```

#### kasan\_init (sys/kern/subr\_asan.c:129)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        load_fs
        kcsan_cpu_init
        x86_init_fdt
        kasan_init <-- Here
```

#### kmsan\_init (sys/kern/subr\_msan.c:600)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        kcsan_cpu_init
        x86_init_fdt
        kasan_init
        kmsan_init <-- Here
```

#### TSEXIT (stand/libsa/stand.h:548)

```txt
Control Flow:
btext
    kasan_early_init
    hammer_time
        ...
        x86_init_fdt
        kasan_init
        kmsan_init
        TSEXIT <-- Here

548: #define TSEXIT() TSRAW("EXIT", __func__, NULL)
```
