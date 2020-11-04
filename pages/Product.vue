<template>
  <div id="product">
    <breadcrumbs :category="category" />
    <section class="pt-70">
      <div class="container">
        <div class="row">
          <div class="col-lg-9">
            <div class="row">
              <div class="col-lg-5 col-md-5 mb-xs-30">
                <!-- <div class="fotorama" data-nav="thumbs" data-allowfullscreen="native">
                  <a href="#"><img src="/assets/images/1.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/2.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/3.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/4.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/5.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/6.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/4.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/5.jpg" alt="Stylexpo"></a> <a href="#"><img src="/assets/images/6.jpg" alt="Stylexpo"></a>
                </div> -->
                <product-gallery
                  :offline="getOfflineImage"
                  :gallery="getProductGallery"
                  :configuration="getCurrentProductConfiguration"
                  :product="getCurrentProduct"
                />
              </div>
              <div class="col-lg-7 col-md-7">
                <div class="row">
                  <div class="col-12">
                    <div class="product-detail-main">
                      <div class="product-item-details">
                        <h1 class="product-item-name">
                          {{ getCurrentProduct.name | htmlDecode }}
                        </h1>
                        <div class="rating-summary-block">
                          <div title="53%" class="rating-result">
                            <span style="width:53%" />
                          </div>
                        </div>
                        <div class="price-box" v-if="getCurrentProduct.special_price && parseFloat(getCurrentProduct.original_price_incl_tax) > 0 && !onlyImage">
                          <span class="price">{{ getCurrentProduct.price_incl_tax | price(storeView) }}</span><del class="price old-price">{{ getCurrentProduct.original_price_incl_tax | price(storeView) }}</del>
                        </div>
                        <div class="price-box" v-if="!getCurrentProduct.special_price && parseFloat(getCurrentProduct.price_incl_tax) > 0 && !onlyImage">
                          <span class="price">{{ getCurrentProduct.price_incl_tax | price(storeView) }}</span>
                        </div>
                        <div class="product-info-stock-sku">
                          <div>
                            <label>Availability: </label>
                            <span class="info-deta">In stock ({{ maxQuantity }})</span>
                          </div>
                          <div>
                            <label>SKU: </label>
                            <span class="info-deta">{{ $t('SKU: {sku}', { sku: getCurrentProduct.sku }) }}</span>
                          </div>
                        </div>
                        <div v-html="getCurrentProduct.short_description" />
                        <div v-if="getCurrentProduct.type_id =='configurable'">
                          <div v-for="option in getProductOptions" :key="option.id">
                            <div class="product-size select-arrow input-box select-dropdown mb-20 mt-30">
                              <label>{{ option.label }}</label>
                              <fieldset>
                                <select v-model="selected[option.attribute_code]" @change="changeFilter(selected[option.attribute_code])" class="selectpicker form-control option-drop" id="select-by-size">
                                  <generic-selector
                                    v-for="filter in getAvailableFilters[option.attribute_code]"
                                    :key="filter.id"
                                    :variant="filter"
                                    :selected-filters="getSelectedFilters"
                                  />
                                </select>
                              </fieldset>
                            </div>
                          </div>
                        </div>
                        <div class="mb-20">
                          <div class="product-qty">
                            <label for="qty">Qty:</label>
                            <div class="custom-qty">
                              <button @click="getCurrentProduct.qty > 1 ? getCurrentProduct.qty-- : 1" class="reduced items" type="button">
                                <i class="fa fa-minus" />
                              </button>
                              <product-quantity
                                v-if="getCurrentProduct.type_id !== 'grouped' && getCurrentProduct.type_id !== 'bundle'"
                                v-model="getCurrentProduct.qty"
                                :max-quantity="maxQuantity"
                                :loading="isStockInfoLoading"
                                :is-simple-or-configurable="isSimpleOrConfigurable"
                                :show-quantity="manageQuantity"
                                :check-max-quantity="manageQuantity"
                                @error="handleQuantityError"
                                @input="inputQty"
                                :readonly="readonly"
                              />

                              <button @click="getCurrentProduct.qty < maxQuantity ? getCurrentProduct.qty++ : maxQuantity" class="increase items" type="button">
                                <i class="fa fa-plus" />
                              </button>
                            </div>
                          </div>
                          <div class="bottom-detail cart-button">
                            <ul>
                              <li class="pro-cart-icon">
                                <add-to-cart
                                  :product="getCurrentProduct"
                                  color="true"
                                  :disabled="isAddToCartDisabled"
                                />
                              </li>
                            </ul>
                          </div>
                        </div>
                        <div class="bottom-detail">
                          <ul>
                            <li class="pro-wishlist-icon">
                              <AddToWishlist :product="getCurrentProduct" />
                            </li>
                            <li class="pro-email-icon">
                              <a href="#"><span />Email to Friends</a>
                            </li>
                          </ul>
                        </div>
                        <div class="share-link">
                          <label>Share This : </label>
                          <div class="social-link">
                            <ul class="social-icon">
                              <li><a class="facebook" title="Facebook" href="#"><i class="fa fa-facebook" /></a></li>
                              <li><a class="twitter" title="Twitter" href="#"><i class="fa fa-twitter" /></a></li>
                              <li><a class="linkedin" title="Linkedin" href="#"><i class="fa fa-linkedin" /></a></li>
                              <li><a class="rss" title="RSS" href="#"><i class="fa fa-rss" /></a></li>
                              <li><a class="pinterest" title="Pinterest" href="#"><i class="fa fa-pinterest" /></a></li>
                            </ul>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-3">
            <div class="brand-logo-pro align-center mb-30">
              <img src="/assets/images/brand5.png" alt="Stylexpo">
            </div>
            <div class="sub-banner-block align-center">
              <img src="/assets/images/pro-banner.jpg" alt="Stylexpo">
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="ptb-70">
      <div class="container">
        <div class="product-detail-tab">
          <div class="row">
            <div class="col-lg-12">
              <div id="tabs">
                <ul class="nav nav-tabs">
                  <li><a class="tab-Description selected" title="Description" @click="toggleBlock('description')">Description</a></li>
                  <li><a class="tab-Product-Tags" title="Product-Tags" @click="toggleBlock('tags')">Product-Tags</a></li>
                  <li><a class="tab-Reviews" title="Reviews" @click="toggleBlock('reviews')">Reviews</a></li>
                </ul>
              </div>
              <div id="items">
                <div class="tab_content">
                  <ul>
                    <li>
                      <div class="items-Description selected " ref="description">
                        <div class="Description" v-html="getCurrentProduct.description" />
                      </div>
                    </li>
                    <li>
                      <div class="items-Product-Tags" ref="tags">
                        <strong>Section 1.10.32 of "de Finibus Bonorum et Malorum", written by Cicero in 45 BC</strong><br>
                        Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur
                      </div>
                    </li>
                    <li>
                      <div class="items-Reviews" ref="reviews">
                        <lazy-hydrate when-idle>
                          <reviews
                            :product-name="getCurrentProduct.name"
                            :product-id="getCurrentProduct.id"
                            v-show="isOnline"
                            :product="getCurrentProduct"
                          />
                        </lazy-hydrate>
                      </div>
                    </li>
                    <!-- <li>
                      <div class="items-Reviews" ref="reviews">
                        <div class="comments-area">
                          <h4>Comments<span>(2)</span></h4>
                          <ul class="comment-list mt-30">
                            <li>
                              <div class="comment-user">
                                <img src="/assets/images/comment-user.jpg" alt="Stylexpo">
                              </div>
                              <div class="comment-detail">
                                <div class="user-name">
                                  John Doe
                                </div>
                                <div class="post-info">
                                  <ul>
                                    <li>Fab 11, 2016</li>
                                    <li><a href="#"><i class="fa fa-reply" />Reply</a></li>
                                  </ul>
                                </div>
                                <p>Consectetur adipiscing elit integer sit amet augue laoreet maximus nuncac.</p>
                              </div>
                              <ul class="comment-list child-comment">
                                <li>
                                  <div class="comment-user">
                                    <img src="/assets/images/comment-user.jpg" alt="Stylexpo">
                                  </div>
                                  <div class="comment-detail">
                                    <div class="user-name">
                                      John Doe
                                    </div>
                                    <div class="post-info">
                                      <ul>
                                        <li>Fab 11, 2016</li>
                                        <li><a href="#"><i class="fa fa-reply" />Reply</a></li>
                                      </ul>
                                    </div>
                                    <p>Consectetur adipiscing elit integer sit amet augue laoreet maximus nuncac.</p>
                                  </div>
                                </li>
                                <li>
                                  <div class="comment-user">
                                    <img src="/assets/images/comment-user.jpg" alt="Stylexpo">
                                  </div>
                                  <div class="comment-detail">
                                    <div class="user-name">
                                      John Doe
                                    </div>
                                    <div class="post-info">
                                      <ul>
                                        <li>Fab 11, 2016</li>
                                        <li><a href="#"><i class="fa fa-reply" />Reply</a></li>
                                      </ul>
                                    </div>
                                    <p>Consectetur adipiscing elit integer sit amet augue laoreet maximus nuncac.</p>
                                  </div>
                                </li>
                              </ul>
                            </li>
                            <li>
                              <div class="comment-user">
                                <img src="/assets/images/comment-user.jpg" alt="Stylexpo">
                              </div>
                              <div class="comment-detail">
                                <div class="user-name">
                                  John Doe
                                </div>
                                <div class="post-info">
                                  <ul>
                                    <li>Fab 11, 2016</li>
                                    <li><a href="#"><i class="fa fa-reply" />Reply</a></li>
                                  </ul>
                                </div>
                                <p>Consectetur adipiscing elit integer sit amet augue laoreet maximus nuncac.</p>
                              </div>
                            </li>
                          </ul>
                        </div>
                        <div class="main-form mt-30">
                          <h4>Leave a comments</h4>
                          <form>
                            <div class="row mt-30">
                              <div class="col-md-4 mb-30">
                                <input type="text" placeholder="Name" required>
                              </div>
                              <div class="col-md-4 mb-30">
                                <input type="email" placeholder="Email" required>
                              </div>
                              <div class="col-md-4 mb-30">
                                <input type="text" placeholder="Website" required>
                              </div>
                              <div class="col-12 mb-30">
                                <textarea cols="30" rows="3" placeholder="Message" required />
                              </div>
                              <div class="col-12 mb-30">
                                <button class="btn btn-color" name="submit" type="submit">
                                  Submit
                                </button>
                              </div>
                            </div>
                          </form>
                        </div>
                      </div>
                    </li> -->
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="pb-70">
      <div class="container">
        <div class="product-listing">
          <div class="row">
            <div class="col-12">
              <div class="heading-part mb-40">
                <h2 class="main_title heading">
                  <span>Related Products</span>
                </h2>
              </div>
            </div>
          </div>
          <div class="pro_cat">
            <div class="row">
              <div class="owl-carousel pro-cat-slider">
                <div class="item">
                  <div class="product-item">
                    <div class="main-label new-label">
                      <span>New</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/10.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label sale-label">
                      <span>Sale</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/13.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label new-label">
                      <span>New</span>
                    </div>
                    <div class="main-label sale-label">
                      <span>Sale</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/4.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/5.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label sale-label">
                      <span>Sale</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/6.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/8.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label new-label">
                      <span>New</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/9.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label sale-label">
                      <span>Sale</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/11.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="item">
                  <div class="product-item">
                    <div class="main-label new-label">
                      <span>New</span>
                    </div>
                    <div class="main-label sale-label">
                      <span>Sale</span>
                    </div>
                    <div class="product-image">
                      <a href="product-page.html"> <img src="/assets/images/2.jpg" alt="Stylexpo"> </a>
                      <div class="product-detail-inner">
                        <div class="detail-inner-left align-center">
                          <ul>
                            <li class="pro-cart-icon">
                              <form>
                                <button title="Add to Cart">
                                  <span />Add to Cart
                                </button>
                              </form>
                            </li>
                            <li class="pro-wishlist-icon ">
                              <a href="wishlist.html" title="Wishlist" />
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
                        <span class="price">$80.00</span> <del class="price old-price">$100.00</del>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import i18n from '@vue-storefront/i18n'
import VueOfflineMixin from 'vue-offline/mixin'
import config from 'config'
import RelatedProducts from 'theme/components/core/blocks/Product/Related.vue'
import Reviews from 'theme/components/core/blocks/Reviews/Reviews.vue'
import AddToCart from 'theme/components/core/AddToCart.vue'
import GenericSelector from 'theme/components/core/GenericSelector'
import ColorSelector from 'theme/components/core/ColorSelector.vue'
import SizeSelector from 'theme/components/core/SizeSelector.vue'
import Breadcrumbs from 'theme/components/core/Breadcrumbs.vue'
import ProductAttribute from 'theme/components/core/ProductAttribute.vue'
import ProductQuantity from 'theme/components/core/ProductQuantity.vue'
import ProductLinks from 'theme/components/core/ProductLinks.vue'
import ProductCustomOptions from 'theme/components/core/ProductCustomOptions.vue'
import ProductBundleOptions from 'theme/components/core/ProductBundleOptions.vue'
import ProductGallery from 'theme/components/core/ProductGallery'
import Spinner from 'theme/components/core/Spinner'
import PromotedOffers from 'theme/components/theme/blocks/PromotedOffers/PromotedOffers'
import focusClean from 'theme/components/theme/directives/focusClean'
import WebShare from 'theme/components/theme/WebShare'
import BaseInputNumber from 'theme/components/core/blocks/Form/BaseInputNumber'
import SizeGuide from 'theme/components/core/blocks/Product/SizeGuide'
import AddToWishlist from 'theme/components/core/blocks/Wishlist/AddToWishlist'
import AddToCompare from 'theme/components/core/blocks/Compare/AddToCompare'
import { mapGetters } from 'vuex'
import LazyHydrate from 'vue-lazy-hydration'
import { ProductOption } from '@vue-storefront/core/modules/catalog/components/ProductOption.ts'
import { getAvailableFiltersByProduct, getSelectedFiltersByProduct } from '@vue-storefront/core/modules/catalog/helpers/filters'
import { isOptionAvailableAsync } from '@vue-storefront/core/modules/catalog/helpers/index'
import { localizedRoute, currentStoreView } from '@vue-storefront/core/lib/multistore'
import { htmlDecode } from '@vue-storefront/core/filters'
import { ReviewModule } from '@vue-storefront/core/modules/review'
import { RecentlyViewedModule } from '@vue-storefront/core/modules/recently-viewed'
import { registerModule, isModuleRegistered } from '@vue-storefront/core/lib/modules'
import { onlineHelper, isServer, productJsonLd } from '@vue-storefront/core/helpers'
import { catalogHooksExecutors } from '@vue-storefront/core/modules/catalog-next/hooks'
import ProductPrice from 'theme/components/core/ProductPrice.vue'
import { doPlatformPricesSync } from '@vue-storefront/core/modules/catalog/helpers'
import { filterChangedProduct } from '@vue-storefront/core/modules/catalog/events'

export default {
  components: {
    AddToCart,
    AddToCompare,
    AddToWishlist,
    Breadcrumbs,
    ColorSelector,
    GenericSelector,
    ProductAttribute,
    ProductBundleOptions,
    ProductCustomOptions,
    ProductGallery,
    ProductLinks,
    PromotedOffers,
    RelatedProducts,
    Reviews,
    SizeSelector,
    WebShare,
    SizeGuide,
    LazyHydrate,
    ProductQuantity,
    ProductPrice
  },
  mixins: [ProductOption],
  directives: { focusClean },
  beforeCreate () {
    registerModule(ReviewModule)
    registerModule(RecentlyViewedModule)
  },
  data () {
    return {
      detailsOpen: false,
      maxQuantity: 0,
      quantityError: false,
      isStockInfoLoading: false,
      hasAttributesLoaded: false,
      manageQuantity: true,
      selected: {},
      readonly: false
    }
  },
  computed: {
    ...mapGetters({
      getCurrentCategory: 'category-next/getCurrentCategory',
      getCategoryByParams: 'category-next/getCategoryByParams',
      getCurrentProduct: 'product/getCurrentProduct',
      getProductGallery: 'product/getProductGallery',
      getCurrentProductConfiguration: 'product/getCurrentProductConfiguration',
      attributesByCode: 'attribute/attributeListByCode',
      getCurrentCustomOptions: 'product/getCurrentCustomOptions'
    }),
    getOptionLabel () {
      return (option) => {
        const configName = option.attribute_code ? option.attribute_code : option.label.toLowerCase()
        return this.getCurrentProductConfiguration[configName] ? this.getCurrentProductConfiguration[configName].label : configName
      }
    },
    isOnline (value) {
      return onlineHelper.isOnline
    },
    getProductOptions () {
      if (
        this.getCurrentProduct.errors &&
        Object.keys(this.getCurrentProduct.errors).length &&
        Object.keys(this.getCurrentProductConfiguration).length
      ) {
        return []
      }
      return this.getCurrentProduct.configurable_options
    },
    getOfflineImage () {
      return {
        src: this.getThumbnail(this.getCurrentProduct.image, config.products.thumbnails.width, config.products.thumbnails.height),
        error: this.getThumbnail(this.getCurrentProduct.image, config.products.thumbnails.width, config.products.thumbnails.height),
        loading: this.getThumbnail(this.getCurrentProduct.image, config.products.thumbnails.width, config.products.thumbnails.height)
      }
    },
    getCustomAttributes () {
      return Object.values(this.attributesByCode || [])
        .filter(
          a => a.is_visible && a.is_user_defined && (parseInt(a.is_visible_on_front) || a.is_visible_on_front === true) && this.getCurrentProduct[a.attribute_code]
        )
        .sort((a, b) => { return a.attribute_id > b.attribute_id })
    },
    getAvailableFilters () {
      return getAvailableFiltersByProduct(this.getCurrentProduct)
    },
    getSelectedFilters () {
      return getSelectedFiltersByProduct(this.getCurrentProduct, this.getCurrentProductConfiguration)
    },
    isSimpleOrConfigurable () {
      return ['simple', 'configurable'].includes(this.getCurrentProduct.type_id)
    },
    isAddToCartDisabled () {
      if (this.quantityError || this.isStockInfoLoading) {
        return false
      }

      return this.isOnline && !this.maxQuantity && this.manageQuantity && this.isSimpleOrConfigurable
    },
    storeView () {
      return currentStoreView()
    },
    getJsonLd () {
      return productJsonLd(this.getCurrentProduct, this.getCurrentProductConfiguration.color && this.getCurrentProductConfiguration.color.label, this.$store.state.storeView.i18n.currencyCode, this.getCustomAttributes)
    },
    category () {
      let last_cat_id = this.getCurrentProduct.category[this.getCurrentProduct.category.length - 1].category_id;
      return this.getCategoryByParams({ id: last_cat_id });
    }
  },
  async mounted () {
    this.selected = this.getSelectedFilters;
    await this.$store.dispatch('recently-viewed/addItem', this.getCurrentProduct)
  },
  async asyncData ({ store, route, context }) {
    if (context) context.output.cacheTags.add('product')
    const product = await store.dispatch('product/loadProduct', { parentSku: route.params.parentSku, childSku: route && route.params && route.params.childSku ? route.params.childSku : null })
    const loadBreadcrumbsPromise = store.dispatch('product/loadProductBreadcrumbs', { product })
    if (isServer) await loadBreadcrumbsPromise
    catalogHooksExecutors.productPageVisited(product)
  },
  beforeRouteEnter (to, from, next) {
    if (isServer) {
      next()
    } else {
      next((vm) => {
        vm.getQuantity()
      })
    }
  },
  watch: {
    isOnline: {
      handler (isOnline) {
        if (isOnline) {
          this.getQuantity()
        }
      }
    }
  },
  methods: {
    showDetails (event) {
      this.detailsOpen = true
      event.target.classList.add('hidden')
    },
    notifyOutStock () {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'error',
        message: this.$t(
          'The product is out of stock and cannot be added to the cart!'
        ),
        action1: { label: this.$t('OK') }
      })
    },
    notifyWrongAttributes () {
      this.$store.dispatch('notification/spawnNotification', {
        type: 'warning',
        message: this.$t(
          'No such configuration for the product. Please do choose another combination of attributes.'
        ),
        action1: { label: this.$t('OK') }
      })
    },
    async changeFilter (variant) {
      const selectedConfiguration = Object.assign({ attribute_code: variant.type }, variant)
      await filterChangedProduct(selectedConfiguration, this.$store, this.$router)
      this.getQuantity()
    },
    openSizeGuide () {
      this.$bus.$emit('modal-show', 'modal-sizeguide')
    },
    isOptionAvailable (option) { // check if the option is available
      const currentConfig = Object.assign({}, this.getCurrentProductConfiguration)
      currentConfig[option.type] = option
      return isOptionAvailableAsync(this.$store, { product: this.getCurrentProduct, configuration: currentConfig })
    },
    async getQuantity () {
      if (this.isStockInfoLoading) return // stock info is already loading
      this.isStockInfoLoading = true
      try {
        if (config.products.alwaysSyncPricesClientSide) {
          doPlatformPricesSync([this.getCurrentProduct]);
        }
        const res = await this.$store.dispatch('stock/check', {
          product: this.getCurrentProduct,
          qty: this.getCurrentProduct.qty
        })

        this.manageQuantity = res.isManageStock
        this.maxQuantity = res.isManageStock ? res.qty : null
      } finally {
        this.isStockInfoLoading = false
      }
    },
    handleQuantityError (error) {
      this.quantityError = error
    },
    inputQty (qty) {
      if (qty > this.maxQuantity) {
        this.getCurrentProduct.qty = this.maxQuantity
        this.readonly = true;
      } else if (qty < 1) {
        this.getCurrentProduct.qty = 1;
      } else {
        this.getCurrentProduct.qty = qty;
      }
    },
    toggleBlock (cat_name) {
      let blocks = ['description', 'tags', 'reviews'];
      for (let block of blocks) {
        block === cat_name ? this.$refs[block].style.display = 'block' : this.$refs[block].style.display = 'none';
      }
      // if (this.$refs[cat_name].style.display === 'none' || this.$refs[cat_name].style.display === '') {
      //   this.$refs[cat_name].style.display = 'block';
      // } else {
      //   this.$refs[cat_name].style.display = 'none';
      // }
    }
  },
  metaInfo () {
    const storeView = currentStoreView()
    return {
      /* link: [
        { rel: 'amphtml',
          href: this.$router.resolve(localizedRoute({
            name: this.getCurrentProduct.type_id + '-product-amp',
            params: {
              parentSku: this.getCurrentProduct.parentSku ? this.getCurrentProduct.parentSku : this.getCurrentProduct.sku,
              slug: this.getCurrentProduct.slug,
              childSku: this.getCurrentProduct.sku
            }
          }, storeView.storeCode)).href
        }
      ], */
      title: htmlDecode(this.getCurrentProduct.meta_title || this.getCurrentProduct.name),
      meta: this.getCurrentProduct.meta_description ? [{ vmid: 'description', name: 'description', content: htmlDecode(this.getCurrentProduct.meta_description) }] : []
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/css/variables/colors';
@import '~theme/css/helpers/functions/color';
$color-primary: color(primary);
$color-tertiary: color(tertiary);
$color-secondary: color(secondary);
$color-white: color(white);
$bg-secondary: color(secondary, $colors-background);

.product {
  &__add-to-compare {
    display: none;
    @media (min-width: 767px) {
      display: block;
    }
  }
}

.breadcrumbs {
  @media (max-width: 767px) {
    margin: 15px 0;
    padding: 15px 0 0 15px;
  }
}

.error {
  color: red;
  font-weight: bold;
  padding-bottom: 15px;
}
.data {
  @media (max-width: 767px) {
    border-bottom: 1px solid $bg-secondary;
  }
}

.image {
  @media (max-width: 1023px) {
    margin-bottom: 20px;
  }
}

.product-name {
  @media (max-width: 767px) {
    font-size: 36px;
  }
}

.variants-label {
  @media (max-width: 767px) {
    font-size: 14px;
  }
}

.variants-wrapper {
  @media (max-width: 767px) {
    padding-bottom: 30px;
  }

  .sizes {
    @media (max-width: 767px) {
      width: 100%;
    }
  }

  .size-guide {
    height: 40px;
    @media (max-width: 767px) {
      width: 100%;
      margin-left: 0;
    }
  }
}

.product-top-section {
  @media (max-width: 767px) {
    padding: 0;
    background-color: $color-white;
  }
}

.add-to-buttons {
  @media (max-width: 767px) {
    padding-top: 30px;
    margin-bottom: 40px;
  }
}

.details {
  @media (max-width: 767px) {
    padding: 50px 15px 15px;
  }
}

.details-title {
  padding: 0 8px;

  @media (max-width: 767px) {
    font-size: 18px;
    margin: 0;
  }
}

.details-wrapper {
  @media (max-width: 767px) {
    position: relative;
    max-height: 140px;
    overflow: hidden;
    transition: all 0.3s ease;
    font-size: 14px;
  }

  &--open {
    max-height: none;
  }
}

.details-overlay {
  @media (max-width: 767px) {
    position: absolute;
    height: 75%;
    bottom: 0;
    left: 0;
    width: 100%;
    margin: 0;
    cursor: pointer;
    background: linear-gradient(rgba($color-white, 0), rgba($color-white, 1));
    &.hidden {
      display: none;
    }
  }
}

.action {
  &:hover {
    color: $color-tertiary;
  }
}

.attributes {
  list-style-type: none;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.product-image {
  mix-blend-mode: multiply;
  width: 460px;
}

.web-share {
  float: right;
}
</style>
