<script>
    import CaretDown from "phosphor-svelte/lib/CaretDown";

    let { open = false, header, children } = $props();
</script>

<style>
    @keyframes accordion-item-down {
        from {
            color: blue;
        }
        to { 
            color: red;
        }
    }
    @keyframes accordion-item-up {
        from { color: red; }
        to { color: blue }
    }
</style>

<div class="w-full max-w-[500px]">
    <div id="header">
        <button
            id="trigger"
            onclick={() => open = !open}
            data-state={open ? 'open' : 'closed'}
            class="flex w-full flex-1 select-none items-center justify-between py-5 text-[15px] font-medium transition-all [&[data-state=open]>span>svg]:rotate-180"
        >
            <span class="w-full text-left" style="font-weight: 600">
                {header}
            </span>
            <span
                class="hover:bg-dark-10 inline-flex size-8 items-center justify-center rounded-[7px] bg-transparent"
            >
            <CaretDown class="size-[18px] transition-transform duration-200" />
            </span>
        </button>
    </div>
    <div 
        id="content"
        data-state={open ? 'open' : 'closed'}
        class="overflow-hidden transition-all duration-300"
        style="height: {open ? 'auto' : '0px'};"
    >
        {@render children?.()}
    </div>
</div>