<script context="module" lang="ts">
	export const prerender = true;
	import Highlight from "svelte-highlight";
	import cpp from "svelte-highlight/src/languages/cpp";
	import materialDarker from "svelte-highlight/src/styles/material-darker";

	const code = `typedef enum GICRegisterOffsets
{
	/*  Distributor register map */
	GICD_CTLR = 0x00,
	GICD_TYPER = 0x04,
	GICD_IIDR = 0x08,

	/* Array of 32 registers each */
	GICD_IGROUPR = 0x080,
	GICD_ISENABLER = 0x100,
	GICD_ICENABLER = 0x180,
	GICD_ISPENDR = 0x200,
	GICD_ICPENDR = 0x280,
	GICD_ISACTIVER = 0x300,
	GICD_ICACTIVER = 0x380,
	GICD_IPRIORITYR = 0x400,

	GICD_ITARGETSR = 0x800,
	GICD_ICFGR = 0xC00,

	GICD_NSCAR = 0xE00,
	GICD_SGIR = 0xF00,

	GICD_CPENDSGIR = 0xF10,
	GICD_SPENDSGIR = 0xF20,

	/* CPU interface register map */
	GICC_CTLR = 0x00,
	GICC_PMR = 0x04,
	GICC_BPR = 0x08,
	GICC_IAR = 0x0C,
	GICC_EOIR = 0x10,
	GICC_RPR = 0x14,
	GICC_HPPIR = 0x18,
	GICC_ABPR = 0x1C,
	GICC_AIAR = 0x20,
	GICC_AEOIR = 0x24,
	GICC_AHPPIR = 0x28,
	GICC_APR = 0xD0,
	GICC_NSAPR = 0xE0,
	GICC_IIDR = 0xFC,
	GICC_DIR = 0x1000,
}GICRegisterOffsets;`;
</script>

<svelte:head>
	<title>AArch64 MMU Programming</title>
	{@html materialDarker}
</svelte:head>

<section>
	<div>
		<h1>
			ARM GIC Programming
		</h1>
	</div>

	<article>
		<p>
			For the development of <a href="https://github.com/bschnepp/pantheon">pantheon</a>, one of the most important peripherals to utilize is the Generic Interrupt Controller.
			For this article, I'll be focusing on the GIC version 2, since it's natively supported by QEMU and the Raspberry Pi 4. All of the relevant code can be found under the path <strong>arch/aarch64/gic.cpp</strong>
		</p>

		<p>
			While there are many different kinds of interrupt controllers a computer system can have: x86 PCs for example will have at least the Intel 8259 PIC controllers, 
			but will also probably have an APIC as well, and embedded ARM microcontrollers will probably have something like the NVIC interrupt controller. Some ARM devices might even have a different interrupt controller entirely, but luckilly these seem to be rare, other than the earlier Raspberry Pis.
			For systems on a chip implementing one or more application-class ARM processors, the GIC is very common to find. It's present on the Raspberry Pi 4, some Rockchip boards, and on at least some NVidia Tegra boards, among many others.
			Fortunately, programming this interrupt controller is actually fairly straightforward, and it's documentation is very complete!
		</p>

		<p>
			Under an operating system, some number of applications need to be run. There's several ways that these can be scheduled, but the most convenient to prevent system deadlock is pre-emptive scheduling.
			This works by having a timer of some sort interrupting the processor at some point, which then signals the kernel to save the current context of the running program, and then try to switch to a different program.
			For pantheon, this is implemented by using the system timer, which then signals an interrupt. This interrupt is then recieved by the GIC, which then is recieved by a processor, switching it back to kernel mode, and then allowing it to handle the interrupt.
		</p>

		<p>
			A simplified view of the registers GIC is present below.
		</p>

		<Highlight language={cpp} {code} />

		<p>
			text3
		</p>
	</article>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}
</style>