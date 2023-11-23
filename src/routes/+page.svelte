<script>
    import Header from "$root/components/Header.svelte"
    import axios from 'axios';
    import {onMount} from 'svelte'

    let menus = []
    let activeMenuItem = null
    let activeFoods = []
    let cartItems = []

    function setActiveItem(item, foods) {
        activeMenuItem = item
        activeFoods = foods ? foods : []
        console.log("activeMenuItem: " + activeMenuItem)
        console.log("activeFoods: " + activeFoods)
    }

    let class_cart = "cart-side-close"
    // const handleCheckout = () => {
    //     class_cart = "cart-side";
    // };
    const handlePayment = () => {
        class_cart = "cart-side-close";
    };
    function addCartItem(id, name, price, qty) {
        const existingItem = cartItems.findIndex(item => item.id === id)
        console.log("existingItem: "+existingItem)
        if (existingItem >= 0) {
            cartItems[existingItem].qty += qty
        } else {
            cartItems = [...cartItems, {
                id: id, name: name, price: price, qty: qty
            }];
        }

        class_cart = cartItems ? "cart-side" : "cart-side-close";
        console.log("cartItems: "+cartItems[0].id);
        console.log(cartItems);
    }

    async function get_menu() {
        var config = {
        method: 'get',
        url: 'http://localhost:8001/menu',
        headers: { 
            'Authorization': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2OTA1MzU4NTQsInJvbGUiOiJhZG1pbiIsInVzZXJuYW1lIjoicnlkaCJ9.5wTyDaHO_eTHwmit4-XElq-VD4p0yXwp1f4MUP_oWDI', 
            'Content-Type': 'application/json'
        }
        };

        axios(config)
            .then(function (response) {
                menus = response.data.data
                activeMenuItem = menus[0].name
                activeFoods = menus[0].foods
                console.log(response.data.data);
            })
            .catch(function (error) {
                console.log(error);
            });
    }

    onMount(async() => {
        await get_menu()
    })
</script>

<Header></Header>
<!-- home section -->
<section class="home" id="home">
    <div class="home-text">
        <h1><span>Selamat datang</span> di mie pedas nomor 1 di Indonesia</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Mauris in aliquam sem fringilla ut morbi tincidunt. Sit amet nisl purus in mollis nunc.</p>
        <a href="#menu" class="btn">Pesan Sekarang</a>
    </div>
    <div class="home-image">
        <img alt="asdf" src="src/images/spaghetti.png">
    </div>
</section>

<section class="menu" id="menu">
    <div class="menu-side">
        <div class="main-text">
            <h2>Menu Terbaik Kami</h2>
            {#each menus as item (item)}
                <a href="#menu" on:click={() => setActiveItem(item.name, item.foods)} class:selected={item.name === activeMenuItem}>{item.name}</a>
            {/each}
        </div>
        <div class="menu-content">
            {#each  activeFoods as food}
                <div class="row">
                    <img alt="asdf" src="src/images/m2.png">
                    <h3>{food.name.toLowerCase()}</h3>
                    <p>Mie dengan sensasi rasa pedas manis dan gurihs</p>
                    <div class="in-text">
                        <div class="price">
                            <h6>Rp. {parseInt(food.price, 10).toLocaleString()}</h6>
                        </div>
                        <div class="s-btn">
                            <a href="#menu" on:click={() => addCartItem(food.id, food.name, food.price, 1)}>Pesan</a>
                        </div>
                    </div>
                </div>
            {/each}
        </div>
    </div>
    <div class="{class_cart}">
        <div class="cart-header">
            <h4>Pesanan Anda</h4>
            <p>Jumat, 10 Feb 2023</p>
        </div>
        <div class="cart-content">
            {#each cartItems as ci }
                <div class="cart-items">
                    <img alt="cart_item" src="src/images/m2.png">
                    <div class="cc-text">
                        <h5>{ci.name}</h5>
                        <h5>Rp {parseInt(ci.price, 10).toLocaleString()}</h5>
                    </div>
                    <div class="cc-qty">
                        <span class="minus">-</span>
                        <input type="text" class="num" value={ci.qty}>
                        <span class="plus">+</span>
                    </div>
                </div>
            {/each}
            <!-- <div class="cart-items">
                <img alt="asdf" src="src/images/m1.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div> -->
            <!-- <div class="cart-items">
                <img alt="asdf" src="src/images/m1.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div>

            <div class="cart-items">
                <img alt="asdf" src="src/images/m2.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div>

            <div class="cart-items">
                <img alt="asdf" src="src/images/m3.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div>

            <div class="cart-items">
                <img alt="asdf" src="src/images/m4.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div>

            <div class="cart-items">
                <img alt="asdf" src="src/images/m2.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div>

            <div class="cart-items">
                <img alt="asdf" src="src/images/m3.png">
                <div class="cc-text">
                    <h5>Mie Gacoan Super</h5>
                    <h5>Rp 10.000</h5>
                </div>
                <div class="cc-qty">
                    <span class="minus">-</span>
                    <input type="text" class="num">
                    <span class="plus">+</span>
                </div>
            </div> -->
        </div>
        <div class="cart-payment">
            <div class="cc-sub">
                <h5>Sub Total</h5>
                <h5>Rp 100.000</h5>
            </div>
            <div class="cc-sub">
                <h5>Ppn</h5>
                <h5>Rp 10.000</h5>
            </div>
            <div class="cc-total">
                <h5>Total</h5>
                <h5>Rp 110.000</h5>
            </div>
            <div class="cc-btn">
                <a href="#menu" on:click={handlePayment}>Bayar</a>
            </div>
        </div>
    </div>
</section>