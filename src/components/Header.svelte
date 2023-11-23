<script>
    import { onMount, onDestroy } from 'svelte';
    import { afterUpdate } from 'svelte';

    let isScrolled = false;

    const handleScroll = () => {
        isScrolled = window.scrollY > 0;
    };

    onMount(() => {
        console.log("qwerqwer")
        window.addEventListener('scroll', handleScroll);
        console.log("asdfasdf")
    });

    afterUpdate(() => {
        window.addEventListener('scroll', handleScroll);
    });

    // onDestroy(() => {
    //     window.removeEventListener('scroll', handleScroll);
    // });
</script>

<header class:scrolled={isScrolled}>
    <img src="src/images/logo.png" alt="Logo" class="logo">

    <ul class="navlist">
        <li><a href="#home">Home</a></li>
        <li><a href="#menu">Menu</a></li>
        <li><a href="#menu">Order</a></li>
        <li><a href="#menu">Contact</a></li>
    </ul>

    <div class="bx bx-menu" id="menu-icon"></div>
</header>