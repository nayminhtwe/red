<template>
  <header class="navbar navbar-custom container-full-sm" id="header">
    <div class="header-top">
      <div class="container">
        <div class="row">
          <div class="col-6">
            <div class="top-link top-link-left select-dropdown">
              <fieldset>
                <select name="speed" class="countr option-drop">
                  <option selected="selected">
                    English
                  </option>
                  <option>Frence</option>
                  <option>German</option>
                </select>
                <select name="speed" class="currenc option-drop">
                  <option selected="selected">
                    USD
                  </option>
                  <option>EURO</option>
                  <option>POUND</option>
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
        <hr>
        <div class="row">
          <div class="col-xl-3 col-md-3 col-xl-20per">
            <div class="header-middle-left">
              <div class="navbar-header float-none-sm">
                <a class="navbar-brand page-scroll" href="index.html">
                  <img alt="Stylexpo" src="/assets/images/logo.png">
                </a>
              </div>
            </div>
          </div>
          <div class="col-xl-6 col-md-6 col-xl-60per">
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
          <div class="col-xl-3 col-md-3 col-xl-20per">
            <div class="right-side float-left-xs header-right-link">
              <ul>
                <li class="compare-icon">
                  <a href="compare.html">
                    <span />
                  </a>
                </li>
                <li class="wishlist-icon">
                  <a href="wishlist.html">
                    <span />
                  </a>
                </li>
                <li class="cart-icon">
                  <a href="#"> <span />
                    <div class="my-cart">2 items<br>$99.00</div>
                  </a>
                  <div class="cart-dropdown header-link-dropdown">
                    <ul class="cart-list link-dropdown-list">
                      <li>
                        <a class="close-cart"><i class="fa fa-times-circle" /></a>
                        <div class="media">
                          <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/1.jpg"></a>
                          <div class="media-body">
                            <span><a href="#">Black African Print Skirt</a></span>
                            <p class="cart-price">
                              $14.99
                            </p>
                            <div class="product-qty">
                              <label>Qty:</label>
                              <div class="custom-qty">
                                <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                              </div>
                            </div>
                          </div>
                        </div>
                      </li>
                      <li>
                        <a class="close-cart"><i class="fa fa-times-circle" /></a>
                        <div class="media">
                          <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/2.jpg"></a>
                          <div class="media-body">
                            <span><a href="#">Black African Print Skirt</a></span>
                            <p class="cart-price">
                              $14.99
                            </p>
                            <div class="product-qty">
                              <label>Qty:</label>
                              <div class="custom-qty">
                                <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                              </div>
                            </div>
                          </div>
                        </div>
                      </li>
                    </ul>
                    <p class="cart-sub-totle">
                      <span class="pull-left">Cart Subtotal</span> <span class="pull-right"><strong class="price-box">$29.98</strong></span>
                    </p>
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
      <div class="container">
        <div class="row position-r">
          <div class="col-xl-2 col-lg-3 col-xl-20per position-s">
            <div class="sidebar-menu-dropdown home">
              <a class="btn-sidebar-menu-dropdown"><span /> Categories </a>
              <div id="cat" class="cat-dropdown">
                <div class="sidebar-contant">
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
                    <ul class="nav navbar-nav ">
                      <li class="level sub-megamenu">
                        <span class="opener plus" />
                        <a href="shop.html" class="page-scroll"><i class="fa fa-female" />Fashion</a>
                        <div class="megamenu mobile-sub-menu " style="width:430px;">
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
                                    <a href="shop.html"><span>■</span>Trousers</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Purse</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Wallets</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Skirts</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Tops</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Sleepwear</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Jeans</a>
                                  </li>
                                </ul>
                              </li>
                              <li class="level2">
                                <div class="sub-menu-slider d-none d-lg-block ">
                                  <div class="row">
                                    <div class="owl-carousel sub_menu_slider">
                                      <div class="product-item">
                                        <div class="product-image">
                                          <a href="product-page.html">
                                            <img src="/assets/images/2.jpg" alt="Stylexpo">
                                          </a>
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
                                          <a href="product-page.html">
                                            <img src="/assets/images/6.jpg" alt="Stylexpo">
                                          </a>
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
                                          <a href="product-page.html">
                                            <img src="/assets/images/8.jpg" alt="Stylexpo">
                                          </a>
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
                                          <a href="product-page.html">
                                            <img src="/assets/images/10.jpg" alt="Stylexpo">
                                          </a>
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
                                          <a href="product-page.html">
                                            <img src="/assets/images/16.jpg" alt="Stylexpo">
                                          </a>
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
                              </li>
                            </ul>
                          </div>
                        </div>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-camera-retro" />Cameras</a>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll">
                          <i class="fa fa-desktop" />computers<div class="menu-label"><span class="hot-menu"> Hot </span></div>
                        </a>
                      </li>
                      <li class="level sub-megamenu">
                        <span class="opener plus" />
                        <a href="shop.html" class="page-scroll"><i class="fa fa-clock-o" />Wathches</a>
                        <div class="megamenu mobile-sub-menu" style="width:775px;">
                          <div class="megamenu-inner-top">
                            <ul class="sub-menu-level1">
                              <li class="level2">
                                <a href="shop.html"><span>Men Fashion</span></a>
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
                                    <a href="shop.html"><span>■</span>Sleepwear</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Jeans</a>
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
                              <li class="level2 d-none d-lg-block">
                                <a href="shop.html">
                                  <img src="/assets/images/drop_banner.jpg" alt="Stylexpo">
                                </a>
                              </li>
                            </ul>
                          </div>
                        </div>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll">
                          <i class="fa fa-shopping-bag" />Bags<div class="menu-label"><span class="new-menu"> New </span></div>
                        </a>
                      </li>
                      <li class="level sub-megamenu ">
                        <span class="opener plus" />
                        <a href="shop.html" class="page-scroll"><i class="fa fa-tablet" />Smartphones</a>
                        <div class="megamenu mobile-sub-menu" style="width:630px;">
                          <div class="megamenu-inner-top">
                            <ul class="sub-menu-level1">
                              <li class="level2">
                                <a href="shop.html"><span>Women Clothings</span></a>
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
                                    <a href="shop.html"><span>■</span>Sleepwear</a>
                                  </li>
                                  <li class="level3">
                                    <a href="shop.html"><span>■</span>Jeans</a>
                                  </li>
                                </ul>
                              </li>
                              <li class="level2">
                                <a href="shop.html"><span>Men Clothings</span></a>
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
                              <li class="level2">
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
                              </li>
                            </ul>
                          </div>
                        </div>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-bed" />Home & Furniture</a>
                      </li>
                      <li class="level ">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-headphones" />Headphone</a>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-microphone" />Accessories</a>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-heartbeat" />Beauty & Health</a>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-bolt" />Printers & Ink</a>
                      </li>
                      <li class="level">
                        <a href="shop.html" class="page-scroll"><i class="fa fa-plus-square" />More Categories</a>
                      </li>
                    </ul>
                    <div class="header-top mobile">
                      <div class="">
                        <div class="row">
                          <div class="col-12">
                            <div class="top-link top-link-left select-dropdown ">
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
                                Need Help? : 03 233 455 55
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
          <div class="col-xl-6 col-lg-6 col-xl-60per">
            <div class="bottom-inner">
              <div class="position-r">
                <div class="nav_sec position-r">
                  <div class="mobilemenu-title mobilemenu">
                    <span>Menu</span>
                    <i class="fa fa-bars pull-right" />
                  </div>
                  <div class="mobilemenu-content">
                    <ul class="nav navbar-nav" id="menu-main">
                      <li class="active">
                        <a href="index.html"><span>Home</span></a>
                      </li>
                      <li>
                        <a href="shop.html"><span>Shop</span></a>
                      </li>
                      <li>
                        <a href="about.html"><span>About Us</span></a>
                      </li>
                      <li>
                        <a href="blog.html"><span>Blog</span></a>
                      </li>
                      <li>
                        <a href="contact.html"><span>Contact</span></a>
                      </li>
                      <li class="level dropdown ">
                        <span class="opener plus" />
                        <a href="#" class="page-scroll"><span>Pages</span></a>
                        <div class="megamenu mobile-sub-menu">
                          <div class="megamenu-inner-top">
                            <ul class="sub-menu-level1">
                              <li class="level2">
                                <ul class="sub-menu-level2 ">
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
                                    <a href="404.html"><span>■</span>404 Error</a>
                                  </li>
                                  <li class="level3">
                                    <a href="single-blog.html"><span>■</span>Single Blog</a>
                                  </li>
                                  <li class="level3">
                                    <a href="product-page.html"><span>■</span>Product Details</a>
                                  </li>
                                </ul>
                              </li>
                            </ul>
                          </div>
                        </div>
                      </li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-4 col-lg-3 col-xl-20per d-none d-lg-block">
            <div class="right-side float-left-xs header-right-link">
              <div class="offer-btn right-side">
                <a href="shop.html" class="gift-offer">
                  <i class="fa fa-gift" /> Offers
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="popup-links ">
      <div class="popup-links-inner">
        <ul>
          <li class="categories">
            <a class="popup-with-form" href="#categories_popup"><span class="icon" /><span class="icon-text">Categories</span></a>
          </li>
          <li class="cart-icon">
            <a class="popup-with-form" href="#cart_popup"><span class="icon" /><span class="icon-text">Cart</span></a>
          </li>
          <li class="account">
            <a class="popup-with-form" href="#account_popup"><span class="icon" /><span class="icon-text">Account</span></a>
          </li>
          <li class="search">
            <a class="popup-with-form" href="#search_popup"><span class="icon" /><span class="icon-text">Search</span></a>
          </li>
          <li class="scroll scrollup">
            <a href="#"><span class="icon" /><span class="icon-text">Scroll-top</span></a>
          </li>
        </ul>
      </div>
      <div id="popup_containt">
        <div id="categories_popup" class="white-popup-block mfp-hide popup-position">
          <div class="popup-title">
            <h2 class="main_title heading">
              <span>categories</span>
            </h2>
          </div>
          <div class="popup-detail">
            <ul class="cate-inner">
              <li class="level sub-megamenu">
                <span class="opener plus" />
                <a href="shop.html" class="page-scroll"><i class="fa fa-female" />Fashion (10)</a>
                <div class="megamenu  mega-sub-menu">
                  <div class="megamenu-inner-top">
                    <ul class="sub-menu-level1">
                      <li class="level2">
                        <ul class="sub-menu-level2 ">
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Blazer & Coat</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Sport Shoes</a>
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
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Skirts</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Tops</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Sleepwear</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Jeans</a>
                          </li>
                        </ul>
                      </li>
                    </ul>
                  </div>
                </div>
              </li>
              <li class="level">
                <a href="shop.html" class="page-scroll"><i class="fa fa-camera-retro" />Cameras (70)</a>
              </li>
              <li class="level">
                <a href="shop.html" class="page-scroll"><i class="fa fa-desktop" />computers (10)</a>
              </li>
              <li class="level sub-megamenu">
                <span class="opener plus" />
                <a href="shop.html" class="page-scroll"><i class="fa fa-clock-o" />Wathches (15)</a>
                <div class="megamenu mega-sub-menu">
                  <div class="megamenu-inner-top">
                    <ul class="sub-menu-level1">
                      <li class="level2">
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
                            <a href="shop.html"><span>■</span>Sleepwear</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Jeans</a>
                          </li>
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
                <a href="shop.html" class="page-scroll"><i class="fa fa-shopping-bag" />Bags (18)</a>
              </li>
              <li class="level sub-megamenu ">
                <span class="opener plus" />
                <a href="shop.html" class="page-scroll"><i class="fa fa-tablet" />Smartphones (20)</a>
                <div class="megamenu mega-sub-menu">
                  <div class="megamenu-inner-top">
                    <ul class="sub-menu-level1">
                      <li class="level2">
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
                            <a href="shop.html"><span>■</span>Sleepwear</a>
                          </li>
                          <li class="level3">
                            <a href="shop.html"><span>■</span>Jeans</a>
                          </li>
                        </ul>
                      </li>
                      <li class="level2">
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
                <a href="shop.html" class="page-scroll"><i class="fa fa-heart" />Software</a>
              </li>
              <li class="level ">
                <a href="shop.html" class="page-scroll"><i class="fa fa-headphones" />Headphone (12)</a>
              </li>
              <li class="level">
                <a href="shop.html" class="page-scroll"><i class="fa fa-microphone" />Accessories (70)</a>
              </li>
              <li class="level">
                <a href="shop.html" class="page-scroll"><i class="fa fa-bolt" />Printers & Ink</a>
              </li>
              <li class="level">
                <a href="shop.html" class="page-scroll"><i class="fa fa-plus-square" />More Categories</a>
              </li>
            </ul>
          </div>
        </div>
        <div id="cart_popup" class="white-popup-block mfp-hide popup-position">
          <div class="popup-title">
            <h2 class="main_title heading">
              <span>cart</span>
            </h2>
          </div>
          <div class="popup-detail">
            <div class="cart-dropdown ">
              <ul class="cart-list link-dropdown-list">
                <li>
                  <a class="close-cart"><i class="fa fa-times-circle" /></a>
                  <div class="media">
                    <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/1.jpg"></a>
                    <div class="media-body">
                      <span><a href="#">Black African Print Skirt</a></span>
                      <p class="cart-price">
                        $14.99
                      </p>
                      <div class="product-qty">
                        <label>Qty:</label>
                        <div class="custom-qty">
                          <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                        </div>
                      </div>
                    </div>
                  </div>
                </li>
                <li>
                  <a class="close-cart"><i class="fa fa-times-circle" /></a>
                  <div class="media">
                    <a class="pull-left"> <img alt="Stylexpo" src="/assets/images/2.jpg"></a>
                    <div class="media-body">
                      <span><a href="#">Black African Print Skirt</a></span>
                      <p class="cart-price">
                        $14.99
                      </p>
                      <div class="product-qty">
                        <label>Qty:</label>
                        <div class="custom-qty">
                          <input type="text" name="qty" maxlength="8" value="1" title="Qty" class="input-text qty">
                        </div>
                      </div>
                    </div>
                  </div>
                </li>
              </ul>
              <p class="cart-sub-totle">
                <span class="pull-left">Cart Subtotal</span> <span class="pull-right"><strong class="price-box">$29.98</strong></span>
              </p>
              <div class="clearfix" />
              <div class="mt-20">
                <a href="cart.html" class="btn-color btn left-side">Cart</a>
                <a href="checkout.html" class="btn-color btn right-side">Checkout</a>
              </div>
            </div>
          </div>
        </div>
        <div id="account_popup" class="white-popup-block mfp-hide popup-position">
          <div class="popup-title">
            <h2 class="main_title heading">
              <span>Account</span>
            </h2>
          </div>
          <div class="popup-detail">
            <div class="row">
              <div class="col-lg-4">
                <a href="account.html">
                  <div class="account-inner mb-30">
                    <i class="fa fa-user" /><br>
                    <span>Account</span>
                  </div>
                </a>
              </div>
              <div class="col-lg-4">
                <a href="register.html">
                  <div class="account-inner mb-30">
                    <i class="fa fa-user-plus" /><br>
                    <span>Register</span>
                  </div>
                </a>
              </div>
              <div class="col-lg-4">
                <a href="cart.html">
                  <div class="account-inner mb-30">
                    <i class="fa fa-shopping-bag" /><br>
                    <span>Shopping</span>
                  </div>
                </a>
              </div>
              <div class="col-lg-4">
                <a href="account.html#step4">
                  <div class="account-inner">
                    <i class="fa fa-key" /><br>
                    <span>Change Pass</span>
                  </div>
                </a>
              </div>
              <div class="col-lg-4">
                <a href="account.html#step3">
                  <div class="account-inner">
                    <i class="fa fa-history" /><br>
                    <span>history</span>
                  </div>
                </a>
              </div>
              <div class="col-lg-4">
                <a href="login.html">
                  <div class="account-inner">
                    <i class="fa fa-share-square-o" /><br>
                    <span>log out</span>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
        <div id="search_popup" class="white-popup-block mfp-hide popup-position">
          <div class="popup-title">
            <h2 class="main_title heading">
              <span>Search</span>
            </h2>
          </div>
          <div class="popup-detail">
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
      </div>
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
