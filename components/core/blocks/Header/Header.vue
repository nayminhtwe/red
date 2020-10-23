<template>
  <header class="navbar navbar-custom container-full-sm" id="header">
    <div class="header-top">
      <div class="container">
        <div class="row">
          <div class="col-6">
            <div class="top-link top-link-left select-dropdown">
              <fieldset>
                <select name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" style="width: 82px;padding: 10px 5px;">
                  <option selected="selected">
                    <span class="ui-selectmenu-text">English</span>
                  </option>
                  <option>
                    <span class="ui-selectmenu-text">Frence</span>
                  </option>
                  <option>
                    <span class="ui-selectmenu-text">German</span>
                  </option>
                </select>
                <select name="speed" class="ui-selectmenu-button ui-widget ui-state-default ui-corner-all" style="width: 82px;padding: 10px 5px;">
                  <option selected="selected" class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">USD</span>
                  </option>
                  <option class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">EURO</span>
                  </option>
                  <option class="ui-selectmenu-text">
                    <span class="ui-selectmenu-text">POUND</span>
                  </option>
                </select>
              </fieldset>
            </div>
          </div>
          <div class="col-6">
            <div class="top-right-link right-side">
              <ul>
                <li class="login-icon content">
                  <a class="content-link">
                    <span class="content-icon" />
                  </a>
                  <a href="login.html" title="Login">Login</a> or
                  <a href="register.html" title="Register">Register</a>
                  <div class="content-dropdown">
                    <ul>
                      <li class="login-icon">
                        <a href="login.html" title="Login"><i class="fa fa-user" /> Login</a>
                      </li>
                      <li class="register-icon">
                        <a href="register.html" title="Register"><i class="fa fa-user-plus" /> Register</a>
                      </li>
                    </ul>
                  </div>
                </li>
                <li class="track-icon">
                  <a href="" title="Track your order"><span /> Track your order</a>
                </li>
                <li class="gift-icon">
                  <a href="" title="Gift card"><span /> Gift card</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="header-middle">
      <div class="container">
        <div class="row">
          <div class="col-xl-2 col-md-3 col-lgmd-20per">
            <div class="header-middle-left">
              <div class="navbar-header float-none-sm">
                <a class="navbar-brand page-scroll" href="index.html">
                  <img alt="Stylexpo" src="/assets/images/logo.png">
                </a>
              </div>
            </div>
          </div>
          <div class="col-xl-8 col-md-6 col-lgmd-60per">
            <div class="header-right-part">
              <div class="category-dropdown select-dropdown">
                <fieldset>
                  <select id="search-category" class="option-drop" name="search-category">
                    <option value="">
                      All Categories
                    </option>
                    <option value="20">
                      Electronics
                    </option>
                    <option value="26">
                      ■ PC
                    </option>
                    <option value="43">
                      &nbsp;&nbsp;&nbsp;- Dell Inspiron
                    </option>
                    <option value="44">
                      &nbsp;&nbsp;&nbsp;- Hp Notebook
                    </option>
                    <option value="47">
                      &nbsp;&nbsp;&nbsp;- Sony Vio
                    </option>
                    <option value="55">
                      &nbsp;&nbsp;&nbsp;- Samsung Tablet
                    </option>
                    <option value="27">
                      ■ Mac
                    </option>
                    <option value="48">
                      &nbsp;&nbsp;&nbsp;- Desktop Mac
                    </option>
                    <option value="49">
                      &nbsp;&nbsp;&nbsp;- Laptop Mac
                    </option>
                    <option value="50">
                      &nbsp;&nbsp;&nbsp;- Samsung Mac
                    </option>
                    <option value="38">
                      &nbsp;&nbsp;&nbsp;- Android tablets
                    </option>
                    <option value="51">
                      ■ Laptops
                    </option>
                    <option value="52">
                      &nbsp;&nbsp;&nbsp;- Accer laptop
                    </option>
                    <option value="56">
                      &nbsp;&nbsp;&nbsp;- apple ipad
                    </option>
                    <option value="53">
                      &nbsp;&nbsp;&nbsp;- HP Laptop
                    </option>
                    <option value="54">
                      &nbsp;&nbsp;&nbsp;- DELL Laptop
                    </option>
                    <option value="18">
                      jewellery
                    </option>
                    <option value="25">
                      Components
                    </option>
                    <option value="29">
                      ■ Mice and Trackballs
                    </option>
                    <option value="28">
                      ■ Monitors
                    </option>
                    <option value="35">
                      &nbsp;&nbsp;&nbsp;- Desktop
                    </option>
                    <option value="36">
                      &nbsp;&nbsp;&nbsp;- LED
                    </option>
                    <option value="30">
                      ■ Printers
                    </option>
                    <option value="31">
                      ■ Scanners
                    </option>
                    <option value="32">
                      ■ Web Cameras
                    </option>
                    <option value="57">
                      Books
                    </option>
                    <option value="17">
                      Interior
                    </option>
                    <option value="24">
                      Fashion
                    </option>
                    <option value="33">
                      House Hold
                    </option>
                    <option value="34">
                      Accessories
                    </option>
                  </select>
                </fieldset>
              </div>
              <div class="main-search">
                <div class="header_search_toggle desktop-view">
                  <form>
                    <div class="search-box">
                      <input class="input-text" type="text" placeholder="Search entire store here...">
                      <button class="search-btn" />
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-2 col-md-3 col-lgmd-20per">
            <div class="right-side float-left-xs header-right-link">
              <ul>
                <li class="cart-icon">
                  <a href="#">
                    <span> <small class="cart-notification">{{ totalQuantity }}</small> </span>
                    <div class="cart-text">
                      <div class="my-cart">Shopping Cart</div>
                      <div class="total-price" v-for="(segment, index) in totals"
                           :key="index" v-if="segment.code === 'grand_total'"
                      >
                        {{ segment.value | price(storeView) }}
                      </div>
                    </div>
                  </a>
                  <div class="cart-dropdown header-link-dropdown">
                    <ul class="cart-list link-dropdown-list">
                      <product v-for="product in productsInCart" :key="product.server_item_id || product.id" :product="product" component="header" />
                    </ul>
                    <div v-for="(segment, index) in totals" :key="index" v-if="segment.code === 'grand_total'">
                      <p class="cart-sub-totle">
                        <span class="pull-left">
                          {{ segment.title }}
                        </span>
                        <span class="pull-right">
                          <strong class="price-box">
                            {{ segment.value | price(storeView) }}
                          </strong>
                        </span>
                      </p>
                    </div>
                    <div class="clearfix" />
                    <div class="mt-20">
                      <a href="cart.html" class="btn-color btn">Cart</a> <a href="checkout.html" class="btn-color btn right-side">Checkout</a>
                    </div>
                  </div>
                </li>
                <li class="side-toggle">
                  <button data-target=".navbar-collapse" data-toggle="collapse" class="navbar-toggle" type="button">
                    <i class="fa fa-bars" />
                  </button>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="header-bottom">
      <div class="container position-s">
        <div id="menu" class="navbar-collapse collapse">
          <div class="top-right-link mobile right-side">
            <ul>
              <li class="login-icon content">
                <a class="content-link">
                  <span class="content-icon" />
                </a>
                <a href="login.html" title="Login">Login</a> or
                <a href="register.html" title="Register">Register</a>
                <div class="content-dropdown">
                  <ul>
                    <li class="login-icon">
                      <a href="login.html" title="Login"><i class="fa fa-user" /> Login</a>
                    </li>
                    <li class="register-icon">
                      <a href="register.html" title="Register"><i class="fa fa-user-plus" /> Register</a>
                    </li>
                  </ul>
                </div>
              </li>
              <li class="track-icon">
                <a title="Track your order"><span /> Track your order</a>
              </li>
              <li class="gift-icon">
                <a href="" title="Gift card"><span /> Gift card</a>
              </li>
            </ul>
          </div>
          <ul class="nav navbar-nav">
            <li class="level">
              <a href="shop.html" class="page-scroll">Today's Deals</a>
            </li>
            <li class="level dropdown">
              <span class="opener plus" /> <a href="shop.html" class="page-scroll">Women</a>
              <div class="megamenu mobile-sub-menu">
                <div class="megamenu-inner-top">
                  <ul class="sub-menu-level1">
                    <li class="level2 ">
                      <a href="shop.html"><span>Women Cloths</span></a>
                      <ul class="sub-menu-level2">
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Dresses</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Sport Jeans</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Skirts</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Tops</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Phone Cases</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Trousers</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Blazer & Coat</a>
                        </li>
                      </ul>
                    </li>
                    <li class="level2">
                      <a href="shop.html"><span>Women Fashion</span></a>
                      <ul class="sub-menu-level2 ">
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Blazer & Coat</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Sport Shoes</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Sport Jeans</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Skirts</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Phone Cases</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Trousers</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Dresses</a>
                        </li>
                      </ul>
                    </li>
                    <li class="level2">
                      <a href="shop.html"><span>Juniors kid</span></a>
                      <ul class="sub-menu-level2 ">
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Sleepwear</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Jeans</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Phone Cases</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Dresses</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Trousers</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Purse</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Wallets</a>
                        </li>
                      </ul>
                    </li>
                    <li class="level2">
                      <div class="megamenu-inner-bottom mt-20 d-none d-lg-block">
                        <a href="shop.html">
                          <img src="/assets/images/drop_banner.jpg" alt="Stylexpo">
                        </a>
                      </div>
                    </li>
                  </ul>
                </div>
              </div>
            </li>
            <li class="level dropdown">
              <span class="opener plus" /> <a href="shop.html" class="page-scroll">Men</a>
              <div class="megamenu full mobile-sub-menu">
                <div class="container">
                  <div class="megamenu-inner">
                    <div class="megamenu-inner-top">
                      <div class="row">
                        <div class="col-lg-10 left-p">
                          <div class="row">
                            <div class="col-lg-4 level2">
                              <a href="shop.html"><span>Men Fashion</span></a>
                              <ul class="sub-menu-level2 ">
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Blazer & Coat</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Sport Shoes</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Phone Cases</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Trousers</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Purse</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Wallets</a>
                                </li>
                              </ul>
                            </div>
                            <div class="col-lg-4 level2">
                              <a href="shop.html"><span>Juniors kid</span></a>
                              <ul class="sub-menu-level2 ">
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Blazer & Coat</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Sport Shoes</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Phone Cases</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Trousers</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Purse</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Wallets</a>
                                </li>
                              </ul>
                            </div>
                            <div class="col-lg-4 level2">
                              <a href="shop.html"><span>Men Clothings</span></a>
                              <ul class="sub-menu-level2 ">
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Blazer & Coat</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Chinos & Trousers</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Underwear</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Trousers</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Purse</a>
                                </li>
                                <li class="level3">
                                  <a href="shop.html"><span>■</span>Wallets</a>
                                </li>
                              </ul>
                            </div>
                          </div>
                          <div class="row">
                            <div class="col-lg-6 d-none d-lg-block mt-30">
                              <div class="sub-menu-img">
                                <a href="shop.html">
                                  <img src="/assets/images/drop_banner1.jpg" alt="Stylexpo">
                                </a>
                              </div>
                            </div>
                            <div class="col-lg-6 d-none d-lg-block mt-30">
                              <div class="sub-menu-img">
                                <a href="shop.html">
                                  <img src="/assets/images/drop_banner2.jpg" alt="Stylexpo">
                                </a>
                              </div>
                            </div>
                          </div>
                        </div>
                        <div class="col-lg-2 level2 d-none d-lg-block">
                          <div class="sub-menu-slider">
                            <div class="row">
                              <div class="owl-carousel sub_menu_slider">
                                <div class="product-item">
                                  <div class="product-image">
                                    <a href="product-page.html"> <img src="/assets/images/1.jpg" alt="Stylexpo"> </a>
                                    <div class="product-detail-inner">
                                      <div class="detail-inner-left align-center">
                                        <ul>
                                          <li class="pro-cart-icon">
                                            <form>
                                              <button title="Add to Cart">
                                                <span />
                                              </button>
                                            </form>
                                          </li>
                                          <li class="pro-wishlist-icon">
                                            <a href="wishlist.html" title="Wishlist" />
                                          </li>
                                          <li class="pro-compare-icon">
                                            <a href="compare.html" title="Compare" />
                                          </li>
                                        </ul>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="product-item-details">
                                    <div class="product-item-name">
                                      <a href="product-page.html">Defyant Reversible Dot Shorts</a>
                                    </div>
                                    <div class="price-box">
                                      <span class="price">$80.00</span>
                                    </div>
                                    <div class="rating-summary-block right-side">
                                      <div title="53%" class="rating-result">
                                        <span style="width:53%" />
                                      </div>
                                    </div>
                                  </div>
                                </div>
                                <div class="product-item">
                                  <div class="product-image">
                                    <a href="product-page.html"> <img src="/assets/images/2.jpg" alt="Stylexpo"> </a>
                                    <div class="product-detail-inner">
                                      <div class="detail-inner-left align-center">
                                        <ul>
                                          <li class="pro-cart-icon">
                                            <form>
                                              <button title="Add to Cart">
                                                <span />
                                              </button>
                                            </form>
                                          </li>
                                          <li class="pro-wishlist-icon">
                                            <a href="wishlist.html" title="Wishlist" />
                                          </li>
                                          <li class="pro-compare-icon">
                                            <a href="compare.html" title="Compare" />
                                          </li>
                                        </ul>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="product-item-details">
                                    <div class="product-item-name">
                                      <a href="product-page.html">Defyant Reversible Dot Shorts</a>
                                    </div>
                                    <div class="price-box">
                                      <span class="price">$80.00</span>
                                    </div>
                                    <div class="rating-summary-block right-side">
                                      <div title="53%" class="rating-result">
                                        <span style="width:53%" />
                                      </div>
                                    </div>
                                  </div>
                                </div>
                                <div class="product-item">
                                  <div class="product-image">
                                    <a href="product-page.html"> <img src="/assets/images/3.jpg" alt="Stylexpo"> </a>
                                    <div class="product-detail-inner">
                                      <div class="detail-inner-left align-center">
                                        <ul>
                                          <li class="pro-cart-icon">
                                            <form>
                                              <button title="Add to Cart">
                                                <span />
                                              </button>
                                            </form>
                                          </li>
                                          <li class="pro-wishlist-icon">
                                            <a href="wishlist.html" title="Wishlist" />
                                          </li>
                                          <li class="pro-compare-icon">
                                            <a href="compare.html" title="Compare" />
                                          </li>
                                        </ul>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="product-item-details">
                                    <div class="product-item-name">
                                      <a href="product-page.html">Defyant Reversible Dot Shorts</a>
                                    </div>
                                    <div class="price-box">
                                      <span class="price">$80.00</span>
                                    </div>
                                    <div class="rating-summary-block right-side">
                                      <div title="53%" class="rating-result">
                                        <span style="width:53%" />
                                      </div>
                                    </div>
                                  </div>
                                </div>
                                <div class="product-item">
                                  <div class="product-image">
                                    <a href="product-page.html"> <img src="/assets/images/4.jpg" alt="Stylexpo"> </a>
                                    <div class="product-detail-inner">
                                      <div class="detail-inner-left align-center">
                                        <ul>
                                          <li class="pro-cart-icon">
                                            <form>
                                              <button title="Add to Cart">
                                                <span />
                                              </button>
                                            </form>
                                          </li>
                                          <li class="pro-wishlist-icon">
                                            <a href="wishlist.html" title="Wishlist" />
                                          </li>
                                          <li class="pro-compare-icon">
                                            <a href="compare.html" title="Compare" />
                                          </li>
                                        </ul>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="product-item-details">
                                    <div class="product-item-name">
                                      <a href="product-page.html">Defyant Reversible Dot Shorts</a>
                                    </div>
                                    <div class="price-box">
                                      <span class="price">$80.00</span>
                                    </div>
                                    <div class="rating-summary-block right-side">
                                      <div title="53%" class="rating-result">
                                        <span style="width:53%" />
                                      </div>
                                    </div>
                                  </div>
                                </div>
                                <div class="product-item">
                                  <div class="product-image">
                                    <a href="product-page.html"> <img src="/assets/images/5.jpg" alt="Stylexpo"> </a>
                                    <div class="product-detail-inner">
                                      <div class="detail-inner-left align-center">
                                        <ul>
                                          <li class="pro-cart-icon">
                                            <form>
                                              <button title="Add to Cart">
                                                <span />
                                              </button>
                                            </form>
                                          </li>
                                          <li class="pro-wishlist-icon">
                                            <a href="wishlist.html" title="Wishlist" />
                                          </li>
                                          <li class="pro-compare-icon">
                                            <a href="compare.html" title="Compare" />
                                          </li>
                                        </ul>
                                      </div>
                                    </div>
                                  </div>
                                  <div class="product-item-details">
                                    <div class="product-item-name">
                                      <a href="product-page.html">Defyant Reversible Dot Shorts</a>
                                    </div>
                                    <div class="price-box">
                                      <span class="price">$80.00</span>
                                    </div>
                                    <div class="rating-summary-block right-side">
                                      <div title="53%" class="rating-result">
                                        <span style="width:53%" />
                                      </div>
                                    </div>
                                  </div>
                                </div>
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </li>
            <li class="level">
              <a href="shop.html" class="page-scroll">Juniors <div class="menu-label"><span class="hot-menu"> Hot </span></div> </a>
            </li>
            <li class="level dropdown">
              <span class="opener plus" /> <a href="shop.html" class="page-scroll">Kids</a>
              <div class="megamenu mobile-sub-menu">
                <div class="megamenu-inner-top">
                  <ul class="sub-menu-level1">
                    <li class="level2">
                      <a href="shop.html"><span>Kids Fashion</span></a>
                      <ul class="sub-menu-level2 ">
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Blazer & Coat</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Sport Shoes</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Phone Cases</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Trousers</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Purse</a>
                        </li>
                        <li class="level3">
                          <a href="shop.html"><span>■</span>Wallets</a>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </div>
              </div>
            </li>
            <li class="level">
              <a href="shop.html" class="page-scroll">Cloths</a>
            </li>
            <li class="level">
              <a href="shop.html" class="page-scroll">Baby <div class="menu-label"><span class="new-menu"> New </span></div></a>
            </li>
            <li class="level">
              <a href="shop.html" class="page-scroll">Accessories</a>
            </li>
            <li class="level dropdown">
              <span class="opener plus" /> <a href="#" class="page-scroll">Pages</a>
              <div class="megamenu mobile-sub-menu">
                <div class="megamenu-inner-top">
                  <ul class="sub-menu-level1">
                    <li class="level2">
                      <ul class="sub-menu-level2 ">
                        <li class="level3">
                          <a href="about.html"><span>■</span>About Us</a>
                        </li>
                        <li class="level3">
                          <a href="account.html"><span>■</span>Account</a>
                        </li>
                        <li class="level3">
                          <a href="checkout.html"><span>■</span>Checkout</a>
                        </li>
                        <li class="level3">
                          <a href="compare.html"><span>■</span>Compare</a>
                        </li>
                        <li class="level3">
                          <a href="wishlist.html"><span>■</span>Wishlist</a>
                        </li>
                        <li class="level3">
                          <a href="contact.html"><span>■</span>Contact</a>
                        </li>
                        <li class="level3">
                          <a href="404.html"><span>■</span>404 Error</a>
                        </li>
                        <li class="level3">
                          <a href="blog.html"><span>■</span>Blog</a>
                        </li>
                        <li class="level3">
                          <a href="single-blog.html"><span>■</span>Single Blog</a>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </div>
              </div>
            </li>
          </ul>
          <div class="header-top mobile">
            <div class="">
              <div class="row">
                <div class="col-12">
                  <div class="top-link top-link-left select-dropdown">
                    <fieldset>
                      <select name="speed" class="country option-drop">
                        <option selected="selected">
                          English
                        </option>
                        <option>Frence</option>
                        <option>German</option>
                      </select>
                      <select name="speed" class="currency option-drop">
                        <option selected="selected">
                          USD
                        </option>
                        <option>EURO</option>
                        <option>POUND</option>
                      </select>
                    </fieldset>
                  </div>
                </div>
                <div class="col-12">
                  <div class="top-link right-side">
                    <div class="help-num">
                      <i class="fa fa-phone" /> Need Help? : 03 233 455 55
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="popup-links ">
      <div class="popup-links-inner">
        <ul>
          <hamburger-icon />
          <microcart-icon />
          <li class="account">
            <a class="popup-with-form" href="#account_popup"><span class="icon" /><span class="icon-text">Account</span></a>
          </li>
          <search-icon />
          <li class="scroll scrollup">
            <a href="#"><span class="icon" /><span class="icon-text">Scroll-top</span></a>
          </li>
        </ul>
      </div>
      <div id="popup_containt" />
    </div>
  </header>
</template>

<script>
import { mapGetters, mapState } from 'vuex'
import CurrentPage from 'theme/mixins/currentPage'
import AccountIcon from 'theme/components/core/blocks/Header/AccountIcon'
import CompareIcon from 'theme/components/core/blocks/Header/CompareIcon'
import HamburgerIcon from 'theme/components/core/blocks/Header/HamburgerIcon'
import Logo from 'theme/components/core/Logo'
import MicrocartIcon from 'theme/components/core/blocks/Header/MicrocartIcon'
import SearchIcon from 'theme/components/core/blocks/Header/SearchIcon'
import WishlistIcon from 'theme/components/core/blocks/Header/WishlistIcon'
import Product from 'theme/components/core/blocks/Microcart/Product'
import { syncCartWhenLocalStorageChange } from '@vue-storefront/core/modules/cart/helpers'

export default {
  name: 'Header',
  components: {
    AccountIcon,
    CompareIcon,
    HamburgerIcon,
    Logo,
    MicrocartIcon,
    SearchIcon,
    WishlistIcon,
    Product
  },
  mixins: [CurrentPage],
  data () {
    return {
      navVisible: true,
      isScrolling: false,
      scrollTop: 0,
      lastScrollTop: 0,
      navbarHeight: 64
    }
  },
  computed: {
    ...mapState({
      isOpenLogin: state => state.ui.signUp,
      currentUser: state => state.user.current
    }),
    ...mapGetters({
      productsInCart: 'cart/getCartItems',
      totals: 'cart/getTotals',
      totalQuantity: 'cart/getItemsTotalQuantity'
    }),
    isThankYouPage () {
      return this.$store.state.checkout.isThankYouPage
        ? this.$store.state.checkout.isThankYouPage
        : false
    }
  },
  beforeMount () {
    window.addEventListener(
      'scroll',
      () => {
        this.isScrolling = true
      },
      { passive: true }
    )

    setInterval(() => {
      if (this.isScrolling) {
        this.hasScrolled()
        this.isScrolling = false
      }
    }, 250)
  },
  mounted () {
    syncCartWhenLocalStorageChange.addEventListener()
    this.$once('hook:beforeDestroy', () => {
      syncCartWhenLocalStorageChange.removeEventListener()
    })
  },
  methods: {
    gotoAccount () {
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    hasScrolled () {
      this.scrollTop = window.scrollY
      if (
        this.scrollTop > this.lastScrollTop &&
        this.scrollTop > this.navbarHeight
      ) {
        this.navVisible = false
      } else {
        this.navVisible = true
      }
      this.lastScrollTop = this.scrollTop
    }
  }
}
</script>
