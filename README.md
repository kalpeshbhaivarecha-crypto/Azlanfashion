import React, { useState, useEffect, useMemo, useRef } from 'react';
import {
  ShoppingBag,
  Search,
  Menu,
  X,
  Phone,
  Mail,
  Heart,
  Eye,
  Star,
  ShieldCheck,
  Truck,
  RotateCcw,
  Sparkles,
  ArrowRight,
  Filter,
  SlidersHorizontal,
  ChevronDown,
  Trash2,
  Plus,
  Minus,
  CheckCircle,
  AlertTriangle,
  Lock,
  User,
  Key,
  LayoutDashboard,
  Package,
  Layers,
  ClipboardList,
  LogOut,
  Edit,
  ExternalLink,
  MessageCircle,
  TrendingUp,
  Boxes,
  Percent,
  Check,
  Settings,
  Info,
  MapPin,
  Tag,
  Download,
  Printer,
  QrCode,
  Share2,
  Flame,
  Clock,
  Compass,
  Gift,
  Laptop,
  Tablet,
  Droplet,
  Umbrella,
  Wallet,
  Smartphone,
  Radio,
  Navigation,
  Barcode,
  History,
  Crown,
  Coins,
  Scale,
  Video,
  Play,
  Pause,
  Volume2,
  VolumeX,
  Type,
  Award,
  Zap,
  Send,
  RefreshCw,
  Sliders
} from 'lucide-react';

const INITIAL_CATEGORIES = [
  'All',
  'Ladies Bags',
  'Handbags',
  'Sling Bags',
  'Backpacks',
  'Travel Bags',
  'Laptop Bags',
  'School Bags',
  'Wallets',
  'Kids Bags',
  'New Arrivals'
];

const INITIAL_PRODUCTS = [
  {
    id: 'az-001',
    name: 'Royal Heritage Leather Satchel',
    category: 'Handbags',
    price: 2499,
    mrp: 4999,
    stock: 8,
    lowStockThreshold: 3,
    rating: 4.9,
    reviewsCount: 42,
    isFeatured: true,
    isNewArrival: true,
    isActive: true,
    liveViewers: 14,
    material: 'Full Grain Tuscan Tanned Leather',
    weight: '820 grams',
    strapType: 'Detachable & Adjustable 120cm Crossbody',
    laptopCompatibility: 'Up to 11" iPad Pro',
    compartments: '3 Main Sections + 1 Zippered Security Pouch',
    warranty: '1 Year Manufacturer Guarantee',
    bundlePartnerId: 'az-007',
    dimensions: '32cm x 24cm x 12cm',
    fitsInside: ['Tablet / iPad 11"', '500ml Flask', 'Makeup Pouch', 'Compact Umbrella', 'Wallet & Smartphone'],
    images: [
      'https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1548036328-c9fa89d128fa?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1590874103328-eac38a683ce7?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Onyx Black', 'Cognac Tan', 'Olive Green'],
    sizes: ['Medium', 'Large'],
    description: 'Masterfully built from vegetable-tanned full grain leather with hand-burnished 18k gold-toned hardware. Incorporates double-reinforced grab handles, an adjustable crossbody strap, and anti-scratch base studs.'
  },
  {
    id: 'az-002',
    name: 'Metropolitan Sleek Crossbody Sling',
    category: 'Sling Bags',
    price: 1399,
    mrp: 2799,
    stock: 4,
    lowStockThreshold: 5,
    rating: 4.7,
    reviewsCount: 29,
    isFeatured: true,
    isNewArrival: true,
    isActive: true,
    liveViewers: 9,
    material: 'Structured Vegan Textured Leather',
    weight: '410 grams',
    strapType: 'Gold Sliding Chain with Leather Shoulder Pad',
    laptopCompatibility: 'Not Applicable (Fits 6.7" Phone)',
    compartments: 'Dual Gusseted Pockets + 4 RFID Card Slots',
    warranty: '6 Months Replacement Guarantee',
    bundlePartnerId: 'az-007',
    dimensions: '22cm x 16cm x 7cm',
    fitsInside: ['Smartphone (Pro Max)', 'Wallet & Cards', 'Lipstick & Keys', 'AirPods Case'],
    images: [
      'https://images.unsplash.com/photo-1591561954557-26941169b49e?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1566150905458-1bf1fc113f0d?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Jet Black', 'Dusty Rose', 'Champagne Beige'],
    sizes: ['Standard'],
    description: 'A minimalist silhouette tailored for effortless transitions from coffee runs to upscale evening dinners. Ultra-lightweight with an RFID-shielded credit card compartment.'
  },
  {
    id: 'az-003',
    name: 'Executive 15.6" Tech Briefcase',
    category: 'Laptop Bags',
    price: 3199,
    mrp: 5999,
    stock: 12,
    lowStockThreshold: 4,
    rating: 4.9,
    reviewsCount: 68,
    isFeatured: true,
    isNewArrival: false,
    isActive: true,
    liveViewers: 21,
    material: 'Hydrophobic Ballistic Canvas & Nappa Trim',
    weight: '980 grams',
    strapType: 'Ergonomic Memory Foam Padded Strap',
    laptopCompatibility: 'Up to 16" MacBook Pro / 15.6" Windows Laptop',
    compartments: 'Padded Shock Sleeve + 2 Document Files + Charger Dock',
    warranty: '2 Years Comprehensive Coverage',
    bundlePartnerId: 'az-007',
    dimensions: '40cm x 30cm x 9cm',
    fitsInside: ['15.6" or 16" Laptop', 'iPad Pro', 'Charger & Mouse', 'A4 File Folders', '750ml Bottle', 'Wallet & Keys'],
    images: [
      'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1622560480605-d83c853bc5c3?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Espresso Brown', 'Slate Grey'],
    sizes: ['15.6 Inch', '14 Inch'],
    description: 'Engineered for high-performing professionals. Features shock-absorbing velvet laptop sleeve, waterproof ballistic leather trim, and a luggage pass-through strap.'
  },
  {
    id: 'az-004',
    name: 'Voyager Handcrafted Weekend Duffel',
    category: 'Travel Bags',
    price: 3699,
    mrp: 6999,
    stock: 3,
    lowStockThreshold: 3,
    rating: 4.8,
    reviewsCount: 51,
    isFeatured: true,
    isNewArrival: true,
    isActive: true,
    liveViewers: 17,
    material: 'Waxed Oil Pull-Up Cowhide',
    weight: '1.45 kg',
    strapType: 'Reinforced Webbed Leather Shoulder Harness',
    laptopCompatibility: 'Dedicated 14" Slip Compartment',
    compartments: 'Ventilated Shoe Tunnel + Main 45L Cavity + Passport Zip',
    warranty: '2 Years Artisan Guarantee',
    bundlePartnerId: 'az-007',
    dimensions: '52cm x 30cm x 26cm',
    fitsInside: ['Shoes in Separate Vent', '3-4 Days Clothing', '15.6" Laptop', 'Toiletry Kit', '1L Water Bottle'],
    images: [
      'https://images.unsplash.com/photo-1544816155-12df9643f363?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Vintage Tan', 'Midnight Navy'],
    sizes: ['45 Litres'],
    description: 'Generously proportioned weekend holdall with aerated separate shoe compartment, heavy-duty YKK brass zips, and detachable padded shoulder cushion.'
  },
  {
    id: 'az-005',
    name: 'Aurelia Quilted Chain Shoulder Bag',
    category: 'Ladies Bags',
    price: 1899,
    mrp: 3799,
    stock: 2,
    lowStockThreshold: 4,
    rating: 4.9,
    reviewsCount: 94,
    isFeatured: true,
    isNewArrival: false,
    isActive: true,
    liveViewers: 32,
    material: 'Soft Lambskin Feel Vegan Nappa Leather',
    weight: '550 grams',
    strapType: 'Interwoven 24K Gold Plated Sliding Chain',
    laptopCompatibility: 'Compact Clutches only (No laptop)',
    compartments: 'Triple Accordion Storage + Center Zip Divider',
    warranty: '1 Year Hardware & Plating Warranty',
    bundlePartnerId: 'az-007',
    dimensions: '26cm x 18cm x 8cm',
    fitsInside: ['Smartphone', 'Cosmetic Compact', 'Perfume Bottle', 'Card Case & Keys'],
    images: [
      'https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1591561954557-26941169b49e?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Ivory Creme', 'Glossy Obsidian', 'Ruby Wine'],
    sizes: ['Regular'],
    description: 'Timeless chevron diamond quilting accentuated with dual gold-interlaced sliding chains. Perfect statement piece for formal galas and luxury celebrations.'
  },
  {
    id: 'az-006',
    name: 'Urban Explorer Waterproof Backpack',
    category: 'Backpacks',
    price: 1999,
    mrp: 3499,
    stock: 14,
    lowStockThreshold: 5,
    rating: 4.6,
    reviewsCount: 34,
    isFeatured: false,
    isNewArrival: true,
    isActive: true,
    liveViewers: 8,
    material: '900D Matte TPU Coated Ripstop Oxford',
    weight: '720 grams',
    strapType: 'Ventilated Air-Mesh Ergonomic S-Straps',
    laptopCompatibility: 'Padded Compartment for 15.6" Laptops',
    compartments: 'Anti-Theft Hidden Back Pocket + Thermal Bottle Slot',
    warranty: '1 Year Waterproof Seam Guarantee',
    bundlePartnerId: 'az-007',
    dimensions: '44cm x 31cm x 15cm',
    fitsInside: ['15.6" Laptop', 'College Books / Folders', 'Umbrella', '1L Bottle', 'Jacket / Hoodie'],
    images: [
      'https://images.unsplash.com/photo-1546938576-6e6a64f317cc?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1622560480605-d83c853bc5c3?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Charcoal Black', 'Military Olive'],
    sizes: ['28 Litres'],
    description: 'Ergonomic lumbar support with ventilated airflow back cushioning. Features expandable thermal side bottle holders and rain-proof matte finish exterior.'
  },
  {
    id: 'az-007',
    name: 'Imperial RFID Bifold Leather Wallet',
    category: 'Wallets',
    price: 799,
    mrp: 1599,
    stock: 19,
    lowStockThreshold: 5,
    rating: 4.8,
    reviewsCount: 58,
    isFeatured: false,
    isNewArrival: false,
    isActive: true,
    liveViewers: 11,
    material: 'Hand-Glazed Top Grain Cowhide',
    weight: '90 grams',
    strapType: 'Slim Pocket Carry (No strap)',
    laptopCompatibility: 'Pocket accessory',
    compartments: '8 Card Slots + Dual Cash Dividers + Coin Flap',
    warranty: '1 Year Stitching & RFID Mesh Guarantee',
    dimensions: '11cm x 9cm x 1.5cm',
    fitsInside: ['10+ Cards', 'Currency Notes', 'Coins & Sim Pocket'],
    images: [
      'https://images.unsplash.com/photo-1627123424574-724758594e93?auto=format&fit=crop&w=900&q=80',
      'https://images.unsplash.com/photo-1606503829068-d06967fd13e8?auto=format&fit=crop&w=900&q=80'
    ],
    colors: ['Deep Havana Brown', 'Classic Black'],
    sizes: ['Slim'],
    description: 'Ultra-slim profile holding up to 10 cards and dual currency notes. Electromagnetic shielding prevents unauthorized RFID contact skimming.'
  }
];

const REELS_DATA = [
  {
    id: 'reel-1',
    productId: 'az-001',
    productName: 'Royal Heritage Leather Satchel',
    price: 2499,
    category: 'Handbags',
    videoUrl: 'https://assets.mixkit.co/videos/preview/mixkit-woman-holding-a-stylish-handbag-40286-large.mp4',
    posterUrl: 'https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=600&q=80',
    tagline: 'Timeless luxury designed for everyday grace ✨'
  },
  {
    id: 'reel-2',
    productId: 'az-002',
    productName: 'Metropolitan Sleek Crossbody Sling',
    price: 1399,
    category: 'Sling Bags',
    videoUrl: 'https://assets.mixkit.co/videos/preview/mixkit-fashion-model-in-the-city-with-a-shoulder-bag-42353-large.mp4',
    posterUrl: 'https://images.unsplash.com/photo-1591561954557-26941169b49e?auto=format&fit=crop&w=600&q=80',
    tagline: 'Lightweight chic from day coffee to evening glam ☕🌙'
  },
  {
    id: 'reel-3',
    productId: 'az-003',
    productName: 'Executive 15.6" Tech Briefcase',
    price: 3199,
    category: 'Laptop Bags',
    videoUrl: 'https://assets.mixkit.co/videos/preview/mixkit-stylish-man-holding-a-leather-briefcase-walking-in-the-street-43283-large.mp4',
    posterUrl: 'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?auto=format&fit=crop&w=600&q=80',
    tagline: 'Command the boardroom with waterproof Italian design 💼'
  }
];

const INITIAL_COUPONS = [
  { code: 'AZLAN10', type: 'percentage', value: 10, minOrder: 999, description: '10% Instant Festive Off' },
  { code: 'FIRSTBAG', type: 'flat', value: 200, minOrder: 1499, description: 'Flat ₹200 Off for New Customers' },
  { code: 'LUCKY15', type: 'percentage', value: 15, minOrder: 1599, description: 'Wheel Prize: 15% VIP Off' },
  { code: 'FLAT300', type: 'flat', value: 300, minOrder: 2499, description: 'Wheel Prize: Flat ₹300 Off' },
  { code: 'VIPSAJID', type: 'percentage', value: 15, minOrder: 2499, description: '15% VIP Privileged Discount' }
];

const WHEEL_PRIZES = [
  { text: '10% OFF', code: 'AZLAN10', color: '#1c1917', textColor: '#D4AF37' },
  { text: '₹200 OFF', code: 'FIRSTBAG', color: '#D4AF37', textColor: '#0c0a09' },
  { text: '15% OFF', code: 'LUCKY15', color: '#292524', textColor: '#fafaf9' },
  { text: '₹300 OFF', code: 'FLAT300', color: '#78350f', textColor: '#fef3c7' },
  { text: 'FREE GIFT', code: 'AZLAN10', color: '#047857', textColor: '#ffffff' },
  { text: 'TRY AGAIN', code: '', color: '#44403c', textColor: '#e7e5e4' }
];

const INITIAL_ORDERS = [
  {
    id: 'AZL-89104',
    customerName: 'Ayesha Khan',
    phone: '9876543210',
    email: 'ayesha.k@example.com',
    address: 'Flat 402, Green Acres, Bandra West',
    city: 'Mumbai',
    state: 'Maharashtra',
    pincode: '400050',
    awbNumber: 'DEL-BOM-9823192',
    courierPartner: 'Delhivery Express Air',
    items: [
      { id: 'az-001', name: 'Royal Heritage Leather Satchel', price: 2499, qty: 1, color: 'Cognac Tan' }
    ],
    monogramDetails: { text: 'A.K.', style: 'Gold Foil', font: 'Serif Classic' },
    coinsEarned: 249,
    coinsUsed: 0,
    discountAmount: 249,
    giftWrapFee: 49,
    giftMessage: 'Happy Birthday Sis! Hope you love this pure leather bag.',
    totalAmount: 2299,
    paymentMethod: 'UPI / Scan & Pay',
    date: '2026-09-28 14:32',
    status: 'Shipped',
    trackingTimeline: [
      { stage: 'Order Placed', time: '28 Sep 2026, 02:32 PM', detail: 'Received & Verified at Azlan Central', completed: true },
      { stage: 'Packed', time: '28 Sep 2026, 05:10 PM', detail: 'Quality Inspected with Luxury Packaging', completed: true },
      { stage: 'Shipped', time: '29 Sep 2026, 09:40 AM', detail: 'Dispatched via Delhivery Air (AWB: DEL-BOM-9823192)', completed: true },
      { stage: 'Out for Delivery', time: 'Expected by 30 Sep', detail: 'Local Hub Kurla West dispatch unit', completed: false },
      { stage: 'Delivered', time: 'Pending confirmation', detail: 'Consignee OTP verification', completed: false }
    ]
  },
  {
    id: 'AZL-89105',
    customerName: 'Rahul Verma',
    phone: '9988776655',
    email: 'rahul.v@example.com',
    address: 'B-12, Sector 62, Noida',
    city: 'Noida',
    state: 'Uttar Pradesh',
    pincode: '201301',
    awbNumber: 'BD-DEL-401124',
    courierPartner: 'BlueDart Surface Express',
    items: [
      { id: 'az-003', name: 'Executive 15.6" Tech Briefcase', price: 3199, qty: 1, color: 'Slate Grey' }
    ],
    monogramDetails: null,
    coinsEarned: 319,
    coinsUsed: 200,
    discountAmount: 200,
    giftWrapFee: 0,
    giftMessage: '',
    totalAmount: 2799,
    paymentMethod: 'Cash on Delivery (COD)',
    date: '2026-09-29 11:15',
    status: 'Packed',
    trackingTimeline: [
      { stage: 'Order Placed', time: '29 Sep 2026, 11:15 AM', detail: 'Payment verification COD approved', completed: true },
      { stage: 'Packed', time: '29 Sep 2026, 03:30 PM', detail: 'Bubble & Dustbag protected seal', completed: true },
      { stage: 'Shipped', time: 'Pending pickup', detail: 'Handover to BlueDart scheduled', completed: false },
      { stage: 'Out for Delivery', time: 'Upcoming', detail: 'Local hub routing', completed: false },
      { stage: 'Delivered', time: 'Pending', detail: 'Collection of ₹2,799 on delivery', completed: false }
    ]
  }
];

const INITIAL_ABANDONED_CARTS = [
  {
    id: 'ab-101',
    customerName: 'Kavita Mehrotra',
    phone: '9820145620',
    itemNames: 'Royal Heritage Leather Satchel',
    cartValue: 2499,
    abandonedAt: '2 hours ago',
    recovered: false
  },
  {
    id: 'ab-102',
    customerName: 'Imran Qureshi',
    phone: '9711084532',
    itemNames: 'Executive 15.6" Tech Briefcase + Imperial Wallet',
    cartValue: 3998,
    abandonedAt: '5 hours ago',
    recovered: false
  }
];

export default function App() {
  // Navigation & Page routing
  const [currentPage, setCurrentPage] = useState('home');
  const [adminTab, setAdminTab] = useState('overview');

  // Master State
  const [products, setProducts] = useState(INITIAL_PRODUCTS);
  const [categories, setCategories] = useState(INITIAL_CATEGORIES);
  const [orders, setOrders] = useState(INITIAL_ORDERS);
  const [coupons, setCoupons] = useState(INITIAL_COUPONS);
  const [abandonedCarts, setAbandonedCarts] = useState(INITIAL_ABANDONED_CARTS);

  // Cart, Wishlist, Compare, & Loyalty
  const [cart, setCart] = useState([]);
  const [wishlist, setWishlist] = useState(['az-001', 'az-005']);
  const [compareList, setCompareList] = useState(['az-001', 'az-003']);
  const [appliedCoupon, setAppliedCoupon] = useState(null);
  const [couponInput, setCouponInput] = useState('');
  const [isGiftWrapAdded, setIsGiftWrapAdded] = useState(false);
  const [giftCardMessage, setGiftCardMessage] = useState('');
  const [recentlyViewedIds, setRecentlyViewedIds] = useState(['az-001', 'az-002', 'az-003']);

  // Monogram Studio
  const [monogramConfig, setMonogramConfig] = useState({
    enabled: false,
    text: '',
    style: 'Gold Foil',
    font: 'Serif Classic'
  });

  // Loyalty Coins
  const [userCoins, setUserCoins] = useState(380);
  const [coinsApplied, setCoinsApplied] = useState(0);

  // Search & Filter State
  const [searchQuery, setSearchQuery] = useState('');
  const [selectedCategory, setSelectedCategory] = useState('All');
  const [sortBy, setSortBy] = useState('featured');
  const [priceFilter, setPriceFilter] = useState(10000);
  const [onlyInStock, setOnlyInStock] = useState(false);

  // Modals & Panels
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);
  const [isCartOpen, setIsCartOpen] = useState(false);
  const [isWishlistOpen, setIsWishlistOpen] = useState(false);
  const [isCompareModalOpen, setIsCompareModalOpen] = useState(false);
  const [isReelsModalOpen, setIsReelsModalOpen] = useState(false);
  const [activeReelIndex, setActiveReelIndex] = useState(0);
  const [isMuted, setIsMuted] = useState(true);
  const [activeModalProduct, setActiveModalProduct] = useState(null);
  const [isCheckoutOpen, setIsCheckoutOpen] = useState(false);
  const [activeInvoiceOrder, setActiveInvoiceOrder] = useState(null);
  const [activeShippingLabelOrder, setActiveShippingLabelOrder] = useState(null);
  const [notification, setNotification] = useState(null);

  // Tracking & Gamification
  const [isTrackingModalOpen, setIsTrackingModalOpen] = useState(false);
  const [trackingSearchQuery, setTrackingSearchQuery] = useState('');
  const [foundTrackingOrder, setFoundTrackingOrder] = useState(null);

  const [isWheelModalOpen, setIsWheelModalOpen] = useState(false);
  const [isSpinning, setIsSpinning] = useState(false);
  const [wheelRotation, setWheelRotation] = useState(0);
  const [wonPrize, setWonPrize] = useState(null);

  // Quick View details
  const [quickViewImageIndex, setQuickViewImageIndex] = useState(0);
  const [selectedVariantColor, setSelectedVariantColor] = useState('');
  const [selectedVariantSize, setSelectedVariantSize] = useState('');
  const [zoomStyle, setZoomStyle] = useState({ display: 'none' });

  // Pincode checker
  const [pincodeQuery, setPincodeQuery] = useState('');
  const [pincodeResult, setPincodeResult] = useState(null);

  // Admin Auth State
  const [adminUser, setAdminUser] = useState(null);
  const [adminEmailInput, setAdminEmailInput] = useState('workwithsajid@zohomail.in');
  const [adminPasswordInput, setAdminPasswordInput] = useState('');
  const [authError, setAuthError] = useState('');
  const [isAuthLoading, setIsAuthLoading] = useState(false);

  // Admin Product Form State
  const [productFormOpen, setProductFormOpen] = useState(false);
  const [editingProduct, setEditingProduct] = useState(null);

  // Checkout Form State
  const [checkoutData, setCheckoutData] = useState({
    fullName: '',
    mobile: '',
    email: '',
    address: '',
    city: '',
    state: 'Maharashtra',
    pincode: '',
    paymentMethod: 'UPI'
  });

  const showToast = (message, type = 'success') => {
    setNotification({ message, type });
    setTimeout(() => setNotification(null), 3800);
  };

  const recordViewedProduct = (id) => {
    setRecentlyViewedIds((prev) => {
      const filtered = prev.filter((pId) => pId !== id);
      return [id, ...filtered].slice(0, 6);
    });
  };

  const cartSubtotal = useMemo(() => {
    return cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
  }, [cart]);

  const couponDiscount = useMemo(() => {
    if (!appliedCoupon) return 0;
    if (cartSubtotal < (appliedCoupon.minOrder || 0)) return 0;
    if (appliedCoupon.type === 'percentage') {
      return Math.round((cartSubtotal * appliedCoupon.value) / 100);
    }
    return Math.min(appliedCoupon.value, cartSubtotal);
  }, [appliedCoupon, cartSubtotal]);

  const giftWrapFee = isGiftWrapAdded && cart.length > 0 ? 49 : 0;
  const monogramFee = monogramConfig.enabled && monogramConfig.text ? 149 : 0;
  const loyaltyCoinsCashDiscount = Math.min(coinsApplied, cartSubtotal);
  const finalPayable = Math.max(0, cartSubtotal - couponDiscount - loyaltyCoinsCashDiscount + giftWrapFee + monogramFee);

  const filteredProducts = useMemo(() => {
    return products
      .filter((prod) => {
        if (!prod.isActive) return false;
        const matchesSearch =
          prod.name.toLowerCase().includes(searchQuery.toLowerCase()) ||
          prod.category.toLowerCase().includes(searchQuery.toLowerCase());
        const matchesCategory =
          selectedCategory === 'All'
            ? true
            : selectedCategory === 'New Arrivals'
            ? prod.isNewArrival
            : prod.category === selectedCategory;
        const matchesPrice = prod.price <= priceFilter;
        const matchesStock = onlyInStock ? prod.stock > 0 : true;

        return matchesSearch && matchesCategory && matchesPrice && matchesStock;
      })
      .sort((a, b) => {
        if (sortBy === 'price-low') return a.price - b.price;
        if (sortBy === 'price-high') return b.price - a.price;
        if (sortBy === 'rating') return b.rating - a.rating;
        if (sortBy === 'newest') return (b.isNewArrival ? 1 : 0) - (a.isNewArrival ? 1 : 0);
        return (b.isFeatured ? 1 : 0) - (a.isFeatured ? 1 : 0);
      });
  }, [products, searchQuery, selectedCategory, priceFilter, onlyInStock, sortBy]);

  const addToCart = (product, qty = 1, chosenColor = '', chosenSize = '', openDrawer = true) => {
    const liveStock = product.stock;
    if (liveStock <= 0) {
      showToast(`Sorry, ${product.name} is currently out of stock.`, 'error');
      return;
    }

    const color = chosenColor || (product.colors && product.colors[0]) || 'Standard';
    const size = chosenSize || (product.sizes && product.sizes[0]) || 'Standard';

    const existingIndex = cart.findIndex(
      (c) => c.id === product.id && c.selectedColor === color && c.selectedSize === size
    );

    const currentQty = existingIndex > -1 ? cart[existingIndex].quantity : 0;
    if (currentQty + qty > liveStock) {
      showToast(`Only ${liveStock} units available in stock. Cannot add more.`, 'error');
      return;
    }

    if (existingIndex > -1) {
      setCart(cart.map((item, idx) => (idx === existingIndex ? { ...item, quantity: item.quantity + qty } : item)));
    } else {
      setCart([
        ...cart,
        {
          ...product,
          quantity: qty,
          selectedColor: color,
          selectedSize: size
        }
      ]);
    }

    showToast(`Added "${product.name}" to your bag!`);
    if (openDrawer) setIsCartOpen(true);
  };

  const updateCartQuantity = (index, newQty) => {
    const item = cart[index];
    const liveProd = products.find((p) => p.id === item.id);
    const maxStock = liveProd ? liveProd.stock : item.stock;

    if (newQty <= 0) {
      removeCartItem(index);
      return;
    }
    if (newQty > maxStock) {
      showToast(`Only ${maxStock} units currently available.`, 'error');
      return;
    }

    setCart(cart.map((c, i) => (i === index ? { ...c, quantity: newQty } : c)));
  };

  const removeCartItem = (index) => {
    setCart(cart.filter((_, i) => i !== index));
    showToast('Item removed from your bag.');
  };

  const toggleWishlist = (productId) => {
    if (wishlist.includes(productId)) {
      setWishlist(wishlist.filter((id) => id !== productId));
      showToast('Removed from Wishlist', 'info');
    } else {
      setWishlist([...wishlist, productId]);
      showToast('Saved to your Wishlist ❤️');
    }
  };

  const toggleCompare = (productId) => {
    if (compareList.includes(productId)) {
      setCompareList(compareList.filter((id) => id !== productId));
      showToast('Removed from comparison list.');
    } else {
      if (compareList.length >= 3) {
        showToast('You can compare a maximum of 3 bags simultaneously.', 'error');
        return;
      }
      setCompareList([...compareList, productId]);
      showToast('Added to Comparison Matrix ⚖️');
    }
  };

  const handleApplyCoupon = (codeToApply) => {
    const code = (codeToApply || couponInput).trim().toUpperCase();
    if (!code) return;
    const match = coupons.find((c) => c.code === code);
    if (!match) {
      showToast(`Coupon "${code}" is invalid or expired.`, 'error');
      return;
    }
    if (cartSubtotal < match.minOrder) {
      showToast(`Minimum order amount of ₹${match.minOrder} required for ${code}.`, 'error');
      return;
    }
    setAppliedCoupon(match);
    setCouponInput('');
    showToast(`Coupon applied! Saved ₹${match.type === 'percentage' ? Math.round((cartSubtotal * match.value) / 100) : match.value}`);
  };

  const removeCoupon = () => {
    setAppliedCoupon(null);
    showToast('Coupon removed.');
  };

  const handleApplyCoins = () => {
    if (coinsApplied > 0) {
      setCoinsApplied(0);
      showToast('Azlan Coins removed.');
    } else {
      const usable = Math.min(userCoins, cartSubtotal);
      if (usable <= 0) {
        showToast('No coins available to redeem.', 'error');
        return;
      }
      setCoinsApplied(usable);
      showToast(`Redeemed ${usable} Azlan Gold Coins! Saved ₹${usable}.`, 'success');
    }
  };

  const handlePlaceOrder = (e) => {
    e.preventDefault();
    if (cart.length === 0) {
      showToast('Your bag is empty!', 'error');
      return;
    }
    if (!checkoutData.fullName || !checkoutData.mobile || !checkoutData.address || !checkoutData.pincode) {
      showToast('Please complete all required shipping fields.', 'error');
      return;
    }

    for (const item of cart) {
      const prod = products.find((p) => p.id === item.id);
      if (!prod || prod.stock < item.quantity) {
        showToast(`Stock changed for "${item.name}". Only ${prod ? prod.stock : 0} remaining.`, 'error');
        return;
      }
    }

    const orderId = 'AZL-' + Math.floor(100000 + Math.random() * 900000);
    const now = new Date();
    const formattedDate = now.toISOString().replace('T', ' ').slice(0, 16);
    const coinsEarned = Math.round(finalPayable * 0.1);

    const newOrder = {
      id: orderId,
      customerName: checkoutData.fullName,
      phone: checkoutData.mobile,
      email: checkoutData.email || 'N/A',
      address: checkoutData.address,
      city: checkoutData.city || 'India',
      state: checkoutData.state,
      pincode: checkoutData.pincode,
      awbNumber: 'DEL-AWB-' + Math.floor(100000 + Math.random() * 900000),
      courierPartner: 'Delhivery Express Air',
      items: cart.map((c) => ({
        id: c.id,
        name: c.name,
        price: c.price,
        qty: c.quantity,
        color: c.selectedColor,
        size: c.selectedSize
      })),
      monogramDetails: monogramConfig.enabled && monogramConfig.text ? monogramConfig : null,
      coinsEarned: coinsEarned,
      coinsUsed: coinsApplied,
      discountAmount: couponDiscount + coinsApplied,
      giftWrapFee: giftWrapFee,
      giftMessage: isGiftWrapAdded ? giftCardMessage : '',
      totalAmount: finalPayable,
      paymentMethod: checkoutData.paymentMethod === 'UPI' ? 'UPI / Scan & Pay' : 'Cash on Delivery (COD)',
      date: formattedDate,
      status: 'Pending',
      trackingTimeline: [
        { stage: 'Order Placed', time: formattedDate, detail: 'Received & Verified at Azlan Central Hub', completed: true },
        { stage: 'Packed', time: 'In Queue', detail: 'Quality check, monogram stamping & dustbag seal', completed: false },
        { stage: 'Shipped', time: 'Upcoming', detail: 'Express courier handover', completed: false },
        { stage: 'Out for Delivery', time: 'Upcoming', detail: 'Local hub routing', completed: false },
        { stage: 'Delivered', time: 'Upcoming', detail: 'Doorstep handover with OTP', completed: false }
      ]
    };

    setProducts((prev) =>
      prev.map((prod) => {
        const bought = cart.find((c) => c.id === prod.id);
        if (bought) {
          return {
            ...prod,
            stock: Math.max(0, prod.stock - bought.quantity)
          };
        }
        return prod;
      })
    );

    setUserCoins((prev) => prev - coinsApplied + coinsEarned);
    setOrders([newOrder, ...orders]);
    setCart([]);
    setAppliedCoupon(null);
    setCoinsApplied(0);
    setIsGiftWrapAdded(false);
    setGiftCardMessage('');
    setIsCheckoutOpen(false);
    setIsCartOpen(false);

    setActiveInvoiceOrder(newOrder);
    showToast(`Order #${orderId} confirmed successfully! You earned ${coinsEarned} Azlan Coins.`, 'success');
  };

  const handleWhatsAppOrder = (singleProduct = null) => {
    const phoneNumber = '917762067143';
    let message = `*NEW ORDER INQUIRY - AZLAN FASHION*\n`;
    message += `--------------------------------------\n`;

    if (singleProduct) {
      const color = selectedVariantColor || (singleProduct.colors && singleProduct.colors[0]) || 'Standard';
      const size = selectedVariantSize || (singleProduct.sizes && singleProduct.sizes[0]) || 'Standard';
      message += `👜 *Product:* ${singleProduct.name}\n`;
      message += `💰 *Offer Price:* ₹${singleProduct.price.toLocaleString('en-IN')}\n`;
      message += `🎨 *Shade / Size:* ${color} | ${size}\n`;
      message += `📦 *Stock Status:* ${singleProduct.stock > 0 ? `${singleProduct.stock} left in stock` : 'Out of stock'}\n`;
      if (monogramConfig.enabled && monogramConfig.text) {
        message += `🔤 *Monogram:* "${monogramConfig.text}" (${monogramConfig.style})\n`;
      }
    } else {
      if (cart.length === 0) {
        showToast('Your shopping bag is empty!', 'error');
        return;
      }
      message += `🛍️ *Order Items (${cart.length}):*\n`;
      cart.forEach((item, idx) => {
        message += `${idx + 1}. ${item.name} (${item.selectedColor}) x ${item.quantity} = ₹${(item.price * item.quantity).toLocaleString('en-IN')}\n`;
      });
      if (monogramConfig.enabled && monogramConfig.text) {
        message += `🔤 *Monogram Personalized:* "${monogramConfig.text}" in ${monogramConfig.style} (+₹149)\n`;
      }
      if (isGiftWrapAdded) {
        message += `🎁 *Luxury Gift Wrapping:* Yes (+₹49)\n`;
        if (giftCardMessage) message += `📝 *Gift Note:* "${giftCardMessage}"\n`;
      }
      if (couponDiscount > 0) {
        message += `\n🏷️ *Coupon Discount:* -₹${couponDiscount.toLocaleString('en-IN')}\n`;
      }
      if (coinsApplied > 0) {
        message += `🪙 *VIP Coins Redeemed:* -₹${coinsApplied}\n`;
      }
      message += `\n💵 *Total Payable:* ₹${finalPayable.toLocaleString('en-IN')}\n`;
      if (checkoutData.fullName) {
        message += `\n👤 *Customer:* ${checkoutData.fullName}\n`;
        message += `📍 *Delivery Address:* ${checkoutData.address}, ${checkoutData.city || ''} - ${checkoutData.pincode}\n`;
        message += `📱 *Phone:* ${checkoutData.mobile}\n`;
      }
    }

    message += `\nHello Azlan Fashion! Please confirm order dispatch and delivery details.`;
    const encoded = encodeURI(message);
    window.open(`https://wa.me/${phoneNumber}?text=${encoded}`, '_blank');
  };

  const handleRecoverAbandonedCartWhatsApp = (abandonedRecord) => {
    const phoneNumber = `91${abandonedRecord.phone}`;
    let msg = `Hello ${abandonedRecord.customerName}! 👜\n\n`;
    msg += `We noticed you left *${abandonedRecord.itemNames}* in your shopping bag at *Azlan Fashion*.\n`;
    msg += `Use exclusive secret coupon *RECOVER10* for an EXTRA 10% OFF + Free Gift Packaging!\n\n`;
    msg += `Click here to complete your order or chat with our styling concierge. We'd love to deliver this luxury piece to you! ✨`;
    window.open(`https://wa.me/${phoneNumber}?text=${encodeURI(msg)}`, '_blank');
    setAbandonedCarts((prev) =>
      prev.map((a) => (a.id === abandonedRecord.id ? { ...a, recovered: true } : a))
    );
    showToast(`WhatsApp recovery sent to ${abandonedRecord.customerName}!`);
  };

  const handleMouseMoveZoom = (e) => {
    const { left, top, width, height } = e.currentTarget.getBoundingClientRect();
    const x = ((e.clientX - left) / width) * 100;
    const y = ((e.clientY - top) / height) * 100;
    setZoomStyle({
      display: 'block',
      backgroundPosition: `${x}% ${y}%`
    });
  };

  const handleMouseLeaveZoom = () => {
    setZoomStyle({ display: 'none' });
  };

  const handleAdminLogin = (e) => {
    e.preventDefault();
    setAuthError('');
    setIsAuthLoading(true);

    setTimeout(() => {
      if (
        (adminEmailInput.toLowerCase() === 'workwithsajid@zohomail.in' || adminEmailInput === 'admin@azlanfashion.com') &&
        adminPasswordInput.length >= 6
      ) {
        setAdminUser({
          email: adminEmailInput,
          displayName: 'Azlan Master Administrator',
          uid: 'azlan-secure-session-erp'
        });
        showToast('Secure Administrator session established.');
        setCurrentPage('admin-dashboard');
      } else {
        setAuthError('Invalid credentials. Password must be 6+ characters and authorized email.');
      }
      setIsAuthLoading(false);
    }, 400);
  };

  const handleAdminLogout = () => {
    setAdminUser(null);
    setCurrentPage('home');
    showToast('Administrator logged out.');
  };

  const handleQuickStock = (productId, delta) => {
    setProducts((prev) =>
      prev.map((p) => (p.id === productId ? { ...p, stock: Math.max(0, p.stock + delta) } : p))
    );
    showToast('Live inventory updated in real-time.');
  };

  const handleExactStock = (productId, val) => {
    const parsed = parseInt(val, 10);
    if (isNaN(parsed) || parsed < 0) return;
    setProducts((prev) => prev.map((p) => (p.id === productId ? { ...p, stock: parsed } : p)));
  };

  const handleOrderStatusChange = (orderId, newStatus) => {
    setOrders((prev) =>
      prev.map((ord) => {
        if (ord.id === orderId) {
          if (newStatus === 'Cancelled' && ord.status !== 'Cancelled') {
            setProducts((prodList) =>
              prodList.map((p) => {
                const found = ord.items.find((it) => it.id === p.id);
                if (found) {
                  return { ...p, stock: p.stock + (found.qty || 1) };
                }
                return p;
              })
            );
            showToast(`Order #${orderId} Cancelled. Stock restored to inventory!`, 'info');
          }
          return { ...ord, status: newStatus };
        }
        return ord;
      })
    );
    showToast(`Order status updated to "${newStatus}"`);
  };

  const handleDeleteProduct = (productId) => {
    setProducts(products.filter((p) => p.id !== productId));
    showToast('Product removed from catalog.');
  };

  const handleSaveProduct = (prodData) => {
    if (prodData.id) {
      setProducts(products.map((p) => (p.id === prodData.id ? prodData : p)));
      showToast(`Updated "${prodData.name}"`);
    } else {
      const newId = 'az-' + Date.now().toString().slice(-4);
      setProducts([{ ...prodData, id: newId }, ...products]);
      showToast(`New product created: "${prodData.name}"`);
    }
    setProductFormOpen(false);
    setEditingProduct(null);
  };

  const exportOrdersToCSV = () => {
    const headers = ['Order ID', 'Date', 'Customer Name', 'Phone', 'Address', 'Pincode', 'Items', 'Monogram', 'Total Amount', 'Payment Method', 'Status', 'AWB'];
    const rows = orders.map((o) => [
      o.id,
      `"${o.date}"`,
      `"${o.customerName}"`,
      `"${o.phone}"`,
      `"${o.address}, ${o.city}"`,
      `"${o.pincode}"`,
      `"${o.items.map((i) => `${i.name} (x${i.qty})`).join('; ')}"`,
      `"${o.monogramDetails ? o.monogramDetails.text : 'None'}"`,
      o.totalAmount,
      `"${o.paymentMethod}"`,
      `"${o.status}"`,
      `"${o.awbNumber || 'N/A'}"`
    ]);

    const csvContent = 'data:text/csv;charset=utf-8,' + [headers.join(','), ...rows.map((e) => e.join(','))].join('\n');
    const encodedUri = encodeURI(csvContent);
    const link = document.createElement('a');
    link.setAttribute('href', encodedUri);
    link.setAttribute('download', `Azlan_Orders_${new Date().toISOString().slice(0, 10)}.csv`);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    showToast('Orders report downloaded in CSV format.');
  };

  const openProductQuickView = (product) => {
    recordViewedProduct(product.id);
    setActiveModalProduct(product);
    setQuickViewImageIndex(0);
    setSelectedVariantColor(product.colors && product.colors[0] ? product.colors[0] : '');
    setSelectedVariantSize(product.sizes && product.sizes[0] ? product.sizes[0] : '');
    setPincodeResult(null);
  };

  const checkDeliveryPincode = (e) => {
    if (e) e.preventDefault();
    if (!pincodeQuery || pincodeQuery.length !== 6) {
      showToast('Please enter a valid 6-digit Indian PIN code.', 'error');
      return;
    }
    const firstDigit = pincodeQuery.charAt(0);
    let days = '3-4';
    let hub = 'Mumbai Central Logistics Hub';
    if (['1', '2'].includes(firstDigit)) {
      days = '4-5'; hub = 'North India Express Transit';
    } else if (['4', '5'].includes(firstDigit)) {
      days = '2-3'; hub = 'West & Central Express Wing';
    } else if (['6', '7'].includes(firstDigit)) {
      days = '4-5'; hub = 'South & East Transit Corridor';
    }

    setPincodeResult({
      pincode: pincodeQuery,
      status: 'AVAILABLE',
      deliveryDays: days,
      hub: hub,
      codAvailable: true,
      freeShipping: true
    });
    showToast(`Delivery available for PIN ${pincodeQuery}! Estimated transit: ${days} days.`);
  };

  const handleSpinTheWheel = () => {
    if (isSpinning) return;
    setIsSpinning(true);
    setWonPrize(null);

    const winningIdx = Math.floor(Math.random() * 4);
    const degreesPerSlice = 360 / WHEEL_PRIZES.length;
    const extraRotations = 360 * 5;
    const targetSliceDegree = 360 - (winningIdx * degreesPerSlice + degreesPerSlice / 2);
    const finalDegree = wheelRotation + extraRotations + targetSliceDegree;

    setWheelRotation(finalDegree);

    setTimeout(() => {
      setIsSpinning(false);
      const prize = WHEEL_PRIZES[winningIdx];
      setWonPrize(prize);
      if (prize.code) {
        handleApplyCoupon(prize.code);
        showToast(`Congratulations! You won ${prize.text} code: ${prize.code}`, 'success');
      }
    }, 4500);
  };

  return (
    <div className="min-h-screen bg-[#FAF8F5] text-stone-900 font-sans antialiased selection:bg-[#D4AF37]/30 flex flex-col pb-16 md:pb-0">
      {/* Toast Notification Box */}
      {notification && (
        <div className="fixed top-5 right-5 z-[9999] max-w-sm flex items-center gap-3 px-4 py-3 rounded-2xl shadow-2xl border backdrop-blur-md bg-stone-950/95 text-white border-stone-700 animate-slide-in">
          {notification.type === 'error' ? (
            <AlertTriangle className="w-5 h-5 text-rose-400 shrink-0" />
          ) : notification.type === 'info' ? (
            <Info className="w-5 h-5 text-amber-300 shrink-0" />
          ) : (
            <CheckCircle className="w-5 h-5 text-emerald-400 shrink-0" />
          )}
          <span className="text-xs sm:text-sm font-medium">{notification.message}</span>
        </div>
      )}

      {/* Floating Interactive Widget Buttons */}
      <div className="fixed bottom-20 md:bottom-6 right-5 z-40 flex flex-col items-end gap-2.5">
        {/* Reels 'Shop the Look' Floating Bubble */}
        <button
          onClick={() => setIsReelsModalOpen(true)}
          className="bg-gradient-to-r from-purple-900 to-stone-950 text-white p-3 rounded-full shadow-2xl border-2 border-[#D4AF37] flex items-center gap-2 transition hover:scale-105 group"
          title="Watch Reels Lookbook"
        >
          <Video className="w-5 h-5 text-[#D4AF37] animate-pulse" />
          <span className="max-w-0 overflow-hidden whitespace-nowrap group-hover:max-w-xs transition-all duration-300 text-xs font-bold">
            Shop The Look (Reels)
          </span>
        </button>

        {/* Compare Floating Badge */}
        {compareList.length > 0 && (
          <button
            onClick={() => setIsCompareModalOpen(true)}
            className="bg-stone-900 text-[#D4AF37] p-3 rounded-full shadow-2xl border border-stone-700 flex items-center gap-2 transition hover:scale-105"
            title="Compare Bags"
          >
            <Scale className="w-5 h-5" />
            <span className="text-xs font-bold">Compare ({compareList.length})</span>
          </button>
        )}

        {/* Spin Wheel */}
        <button
          onClick={() => setIsWheelModalOpen(true)}
          className="bg-stone-950 text-[#D4AF37] p-3 rounded-full shadow-2xl border-2 border-[#D4AF37] flex items-center gap-2 transition hover:scale-105 group"
          title="Spin the Lucky Wheel"
        >
          <Sparkles className="w-5 h-5 text-[#D4AF37] animate-spin" />
          <span className="max-w-0 overflow-hidden whitespace-nowrap group-hover:max-w-xs transition-all duration-300 text-xs font-bold">
            Spin & Win
          </span>
        </button>

        {/* WhatsApp Concierge */}
        <a
          href="https://wa.me/917762067143?text=Hello%20Azlan%20Fashion,%20I%20need%20assistance%20with%20a%20bag%20order."
          target="_blank"
          rel="noreferrer"
          className="bg-emerald-600 hover:bg-emerald-500 text-white p-3.5 rounded-full shadow-2xl border-2 border-white flex items-center gap-2 transition hover:scale-105 group"
          title="WhatsApp Concierge"
        >
          <MessageCircle className="w-6 h-6" />
          <span className="max-w-0 overflow-hidden whitespace-nowrap group-hover:max-w-xs transition-all duration-300 text-xs font-bold">
            Chat with Azlan
          </span>
        </a>
      </div>

      {/* Top Announcement Bar with VIP Coins info */}
      <div className="bg-stone-950 text-stone-300 text-xs py-2 px-4 border-b border-stone-800">
        <div className="max-w-7xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-1.5">
          <div className="flex items-center gap-2">
            <span className="inline-block w-2 h-2 rounded-full bg-[#D4AF37] animate-pulse"></span>
            <span className="tracking-wide">
              Festive Bag Fair • Use Coupon <strong className="text-[#D4AF37] tracking-wider">AZLAN10</strong> for 10% OFF
            </span>
            <span className="hidden md:inline text-stone-500">•</span>
            <span className="hidden md:inline text-amber-300 text-[11px] font-semibold flex items-center gap-1">
              <Coins className="w-3 h-3 text-[#D4AF37]" /> Your VIP Coins: {userCoins} (₹{userCoins} Cash Discount)
            </span>
          </div>

          <div className="flex items-center gap-4 text-stone-400 text-[11px] sm:text-xs">
            <button
              onClick={() => {
                setFoundTrackingOrder(null);
                setTrackingSearchQuery('');
                setIsTrackingModalOpen(true);
              }}
              className="text-[#D4AF37] hover:underline flex items-center gap-1 font-semibold"
            >
              <Navigation className="w-3 h-3" /> Track Order
            </button>
            <span className="hidden sm:inline">|</span>
            <a href="tel:7762067143" className="flex items-center gap-1 hover:text-[#D4AF37] transition">
              <Phone className="w-3 h-3" /> +91 7762067143
            </a>
            <span className="hidden sm:inline">|</span>
            {adminUser ? (
              <button
                onClick={() => setCurrentPage('admin-dashboard')}
                className="text-[#D4AF37] font-semibold hover:underline flex items-center gap-1"
              >
                <LayoutDashboard className="w-3 h-3" /> Admin ERP
              </button>
            ) : (
              <button
                onClick={() => setCurrentPage('admin-login')}
                className="hover:text-stone-200 text-stone-500 text-[11px]"
              >
                Staff Portal
              </button>
            )}
          </div>
        </div>
      </div>

      {/* Header */}
      <header className="sticky top-0 z-40 bg-white/95 backdrop-blur-md border-b border-stone-200 shadow-xs transition-all">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex items-center justify-between h-20">
            {/* Logo */}
            <div
              className="flex items-center gap-3 cursor-pointer"
              onClick={() => {
                setCurrentPage('home');
                setSelectedCategory('All');
                window.scrollTo({ top: 0, behavior: 'smooth' });
              }}
            >
              <div className="w-10 h-10 rounded-full bg-stone-950 text-[#D4AF37] flex items-center justify-center font-serif text-xl font-bold shadow-inner border border-[#D4AF37]/40">
                A
              </div>
              <div>
                <span className="text-xl sm:text-2xl font-serif font-black tracking-widest uppercase text-stone-950 block leading-tight">
                  Azlan Fashion
                </span>
                <span className="text-[10px] tracking-[0.25em] text-[#C5A059] uppercase block font-medium">
                  Artisanal Bags & Leather
                </span>
              </div>
            </div>

            {/* Desktop Navigation Links */}
            <nav className="hidden md:flex items-center space-x-7 text-sm font-medium tracking-wide text-stone-700">
              <button
                onClick={() => { setCurrentPage('home'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                className={`transition-colors hover:text-[#C5A059] ${currentPage === 'home' ? 'text-stone-950 font-bold border-b-2 border-[#D4AF37] pb-1' : ''}`}
              >
                Home
              </button>
              <button
                onClick={() => { setCurrentPage('shop'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                className={`transition-colors hover:text-[#C5A059] ${currentPage === 'shop' ? 'text-stone-950 font-bold border-b-2 border-[#D4AF37] pb-1' : ''}`}
              >
                Shop All Bags
              </button>
              <button
                onClick={() => setIsReelsModalOpen(true)}
                className="transition-colors hover:text-purple-600 flex items-center gap-1 text-purple-700 font-bold"
              >
                <Video className="w-4 h-4 animate-bounce" /> Reels Lookbook
              </button>
              <button
                onClick={() => { setCurrentPage('categories'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                className={`transition-colors hover:text-[#C5A059] ${currentPage === 'categories' ? 'text-stone-950 font-bold border-b-2 border-[#D4AF37] pb-1' : ''}`}
              >
                Categories
              </button>
              <button
                onClick={() => setIsCompareModalOpen(true)}
                className="transition-colors hover:text-[#C5A059] flex items-center gap-1 font-medium"
              >
                <Scale className="w-3.5 h-3.5 text-[#C5A059]" /> Compare ({compareList.length})
              </button>
              <button
                onClick={() => { setCurrentPage('about'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                className={`transition-colors hover:text-[#C5A059] ${currentPage === 'about' ? 'text-stone-950 font-bold border-b-2 border-[#D4AF37] pb-1' : ''}`}
              >
                About
              </button>
              <button
                onClick={() => { setCurrentPage('contact'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                className={`transition-colors hover:text-[#C5A059] ${currentPage === 'contact' ? 'text-stone-950 font-bold border-b-2 border-[#D4AF37] pb-1' : ''}`}
              >
                Contact
              </button>
            </nav>

            {/* Actions: Search, Wishlist, Cart */}
            <div className="flex items-center gap-2 sm:gap-4">
              <div className="relative hidden sm:block">
                <input
                  type="text"
                  placeholder="Search slings, leather, travel..."
                  value={searchQuery}
                  onChange={(e) => {
                    setSearchQuery(e.target.value);
                    if (currentPage !== 'shop') setCurrentPage('shop');
                  }}
                  className="w-44 lg:w-56 pl-8 pr-3 py-1.5 text-xs rounded-full border border-stone-300 bg-stone-50/80 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
                />
                <Search className="w-3.5 h-3.5 text-stone-400 absolute left-3 top-2.5" />
              </div>

              {/* Wishlist */}
              <button
                onClick={() => setIsWishlistOpen(true)}
                className="relative p-2 rounded-full hover:bg-stone-100 text-stone-800 transition"
                title="Your Wishlist"
              >
                <Heart className="w-5 h-5 text-stone-800" />
                {wishlist.length > 0 && (
                  <span className="absolute -top-0.5 -right-0.5 bg-rose-600 text-white text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center shadow">
                    {wishlist.length}
                  </span>
                )}
              </button>

              {/* Cart */}
              <button
                onClick={() => setIsCartOpen(true)}
                className="relative p-2 rounded-full hover:bg-stone-100 text-stone-800 transition"
                title="Shopping Bag"
              >
                <ShoppingBag className="w-5 h-5 text-stone-900" />
                {cart.length > 0 && (
                  <span className="absolute -top-0.5 -right-0.5 bg-stone-950 text-[#D4AF37] text-[10px] font-bold w-5 h-5 rounded-full flex items-center justify-center border border-white shadow">
                    {cart.reduce((t, i) => t + i.quantity, 0)}
                  </span>
                )}
              </button>

              {/* Mobile Hamburger */}
              <button
                onClick={() => setIsMobileMenuOpen(!isMobileMenuOpen)}
                className="md:hidden p-2 rounded-lg text-stone-700 hover:bg-stone-100"
              >
                {isMobileMenuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
              </button>
            </div>
          </div>
        </div>

        {/* Quick Horizontal Ribbon */}
        <div className="bg-[#FAF8F5] border-t border-stone-200/80 py-2.5 px-4 overflow-x-auto no-scrollbar">
          <div className="max-w-7xl mx-auto flex items-center gap-2 text-xs">
            <span className="font-bold text-stone-500 uppercase tracking-widest text-[10px] shrink-0 mr-1 flex items-center gap-1">
              <Compass className="w-3 h-3 text-[#C5A059]" /> Quick Pick:
            </span>
            {categories.map((cat) => (
              <button
                key={cat}
                onClick={() => {
                  setSelectedCategory(cat);
                  setCurrentPage('shop');
                  window.scrollTo({ top: 320, behavior: 'smooth' });
                }}
                className={`px-3 py-1 rounded-full whitespace-nowrap text-xs font-semibold transition shrink-0 ${
                  selectedCategory === cat && currentPage === 'shop'
                    ? 'bg-stone-950 text-[#D4AF37] shadow-xs'
                    : 'bg-white text-stone-700 border border-stone-200 hover:border-[#D4AF37]'
                }`}
              >
                {cat}
              </button>
            ))}
          </div>
        </div>
      </header>

      {/* Main Pages Switch */}
      <main className="flex-1">
        {currentPage === 'home' && (
          <HomePage
            products={products}
            categories={categories}
            onSelectCategory={(cat) => {
              setSelectedCategory(cat);
              setCurrentPage('shop');
              window.scrollTo({ top: 0, behavior: 'smooth' });
            }}
            onOpenProduct={openProductQuickView}
            onAddToCart={addToCart}
            onToggleWishlist={toggleWishlist}
            wishlist={wishlist}
            onToggleCompare={toggleCompare}
            compareList={compareList}
            onNavigateShop={() => {
              setCurrentPage('shop');
              window.scrollTo({ top: 0, behavior: 'smooth' });
            }}
            onWhatsAppOrder={handleWhatsAppOrder}
            onOpenWheel={() => setIsWheelModalOpen(true)}
            onOpenReels={() => setIsReelsModalOpen(true)}
          />
        )}

        {currentPage === 'shop' && (
          <ShopPage
            products={filteredProducts}
            categories={categories}
            selectedCategory={selectedCategory}
            setSelectedCategory={setSelectedCategory}
            searchQuery={searchQuery}
            setSearchQuery={setSearchQuery}
            sortBy={sortBy}
            setSortBy={setSortBy}
            priceFilter={priceFilter}
            setPriceFilter={setPriceFilter}
            onlyInStock={onlyInStock}
            setOnlyInStock={setOnlyInStock}
            onOpenProduct={openProductQuickView}
            onAddToCart={addToCart}
            onToggleWishlist={toggleWishlist}
            wishlist={wishlist}
            onToggleCompare={toggleCompare}
            compareList={compareList}
            onWhatsAppOrder={handleWhatsAppOrder}
          />
        )}

        {currentPage === 'categories' && (
          <CategoriesExplorerPage
            categories={categories}
            products={products}
            onSelectCategory={(cat) => {
              setSelectedCategory(cat);
              setCurrentPage('shop');
              window.scrollTo({ top: 0, behavior: 'smooth' });
            }}
          />
        )}

        {currentPage === 'about' && <AboutUsPage />}

        {currentPage === 'contact' && <ContactPage onWhatsAppOrder={handleWhatsAppOrder} />}

        {currentPage === 'policies' && <PoliciesPage />}

        {currentPage === 'admin-login' && (
          <AdminLoginPage
            email={adminEmailInput}
            setEmail={setAdminEmailInput}
            password={adminPasswordInput}
            setPassword={setAdminPasswordInput}
            onSubmit={handleAdminLogin}
            error={authError}
            isLoading={isAuthLoading}
            onBackToStore={() => setCurrentPage('home')}
          />
        )}

        {currentPage === 'admin-dashboard' && (
          <AdminDashboardPage
            adminUser={adminUser}
            onLogout={handleAdminLogout}
            adminTab={adminTab}
            setAdminTab={setAdminTab}
            products={products}
            orders={orders}
            categories={categories}
            coupons={coupons}
            abandonedCarts={abandonedCarts}
            onRecoverAbandonedCart={handleRecoverAbandonedCartWhatsApp}
            onQuickStock={handleQuickStock}
            onExactStock={handleExactStock}
            onOrderStatusChange={handleOrderStatusChange}
            onDeleteProduct={handleDeleteProduct}
            onOpenAddProduct={() => {
              setEditingProduct(null);
              setProductFormOpen(true);
            }}
            onOpenEditProduct={(prod) => {
              setEditingProduct(prod);
              setProductFormOpen(true);
            }}
            onAddCategory={(cat) => {
              if (cat && !categories.includes(cat)) {
                setCategories([...categories, cat]);
                showToast(`Category "${cat}" added.`);
              }
            }}
            onDeleteCategory={(cat) => {
              setCategories(categories.filter((c) => c !== cat));
              showToast(`Category "${cat}" removed.`);
            }}
            onExportCSV={exportOrdersToCSV}
            onViewInvoice={(ord) => setActiveInvoiceOrder(ord)}
            onViewShippingLabel={(ord) => setActiveShippingLabelOrder(ord)}
            showToast={showToast}
          />
        )}
      </main>

      {}
      {isReelsModalOpen && (
        <div className="fixed inset-0 z-50 overflow-hidden bg-stone-950/90 backdrop-blur-md flex items-center justify-center p-2 sm:p-4">
          <div className="relative w-full max-w-sm h-[88vh] bg-stone-900 rounded-3xl overflow-hidden shadow-2xl border border-stone-800 flex flex-col justify-between animate-scale">
            {/* Reel Header */}
            <div className="absolute top-4 left-4 right-4 z-20 flex justify-between items-center text-white">
              <div className="flex items-center gap-2 bg-stone-950/60 px-3 py-1 rounded-full backdrop-blur-xs">
                <Video className="w-4 h-4 text-[#D4AF37]" />
                <span className="text-xs font-bold tracking-wider uppercase">Azlan Fashion Lookbook</span>
              </div>
              <button
                onClick={() => setIsReelsModalOpen(false)}
                className="w-8 h-8 rounded-full bg-stone-950/80 text-white flex items-center justify-center hover:bg-stone-800"
              >
                <X className="w-5 h-5" />
              </button>
            </div>

            {/* Video Player */}
            <div className="relative w-full h-full flex items-center justify-center bg-stone-950">
              <video
                key={REELS_DATA[activeReelIndex].id}
                src={REELS_DATA[activeReelIndex].videoUrl}
                poster={REELS_DATA[activeReelIndex].posterUrl}
                autoPlay
                loop
                muted={isMuted}
                playsInline
                className="w-full h-full object-cover"
              />

              <button
                onClick={() => setIsMuted(!isMuted)}
                className="absolute top-16 right-4 z-20 p-2 rounded-full bg-stone-950/70 text-white"
              >
                {isMuted ? <VolumeX className="w-4 h-4" /> : <Volume2 className="w-4 h-4" />}
              </button>
            </div>

            {/* Reel Footer */}
            <div className="absolute bottom-4 left-4 right-4 z-20 space-y-3">
              <div className="p-3 rounded-2xl bg-stone-950/85 backdrop-blur-md border border-stone-700/80 text-white flex items-center justify-between gap-3">
                <div className="min-w-0">
                  <span className="text-[10px] font-bold text-[#D4AF37] uppercase block">
                    {REELS_DATA[activeReelIndex].category}
                  </span>
                  <h4 className="text-xs font-serif font-bold truncate">
                    {REELS_DATA[activeReelIndex].productName}
                  </h4>
                  <p className="text-xs font-black text-white mt-0.5">
                    ₹{REELS_DATA[activeReelIndex].price.toLocaleString('en-IN')}
                  </p>
                </div>
                <button
                  onClick={() => {
                    const prod = products.find((p) => p.id === REELS_DATA[activeReelIndex].productId);
                    if (prod) {
                      addToCart(prod, 1, '', '', true);
                      setIsReelsModalOpen(false);
                    }
                  }}
                  className="px-3.5 py-2 bg-[#D4AF37] hover:bg-[#c49f2b] text-stone-950 font-bold text-xs uppercase rounded-xl tracking-wider shadow-lg shrink-0 flex items-center gap-1.5"
                >
                  <ShoppingBag className="w-3.5 h-3.5" /> Buy Look
                </button>
              </div>

              {/* Reel Navigation Dots */}
              <div className="flex justify-center gap-2">
                {REELS_DATA.map((_, idx) => (
                  <button
                    key={idx}
                    onClick={() => setActiveReelIndex(idx)}
                    className={`h-1.5 rounded-full transition-all ${activeReelIndex === idx ? 'w-6 bg-[#D4AF37]' : 'w-2 bg-stone-600'}`}
                  />
                ))}
              </div>
            </div>
          </div>
        </div>
      )}

      {isCompareModalOpen && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/75 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="relative bg-white rounded-3xl max-w-4xl w-full shadow-2xl overflow-hidden border border-stone-200 p-6 space-y-6 animate-scale">
            <div className="flex justify-between items-center border-b pb-4">
              <div className="flex items-center gap-2.5">
                <div className="w-10 h-10 rounded-2xl bg-stone-950 text-[#D4AF37] flex items-center justify-center">
                  <Scale className="w-5 h-5" />
                </div>
                <div>
                  <h3 className="text-lg font-serif font-bold text-stone-950">Bespoke Bag Comparison Matrix</h3>
                  <p className="text-xs text-stone-500">Compare materials, dimensions, and specifications side-by-side</p>
                </div>
              </div>
              <button onClick={() => setIsCompareModalOpen(false)} className="text-stone-400 hover:text-stone-700">
                <X className="w-5 h-5" />
              </button>
            </div>

            {compareList.length === 0 ? (
              <div className="text-center py-12 text-stone-500 text-xs">
                <Scale className="w-12 h-12 mx-auto text-stone-300 mb-2" />
                <p>No bags selected for comparison. Tap "Compare" on any bag card in the catalog.</p>
              </div>
            ) : (
              <div className="overflow-x-auto">
                <table className="w-full text-xs text-left border-collapse">
                  <thead>
                    <tr className="border-b border-stone-200">
                      <th className="p-3 font-bold text-stone-400 uppercase text-[10px] w-1/4">Bag Specification</th>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        if (!prod) return null;
                        return (
                          <th key={id} className="p-3 text-center align-top">
                            <div className="relative inline-block mb-2">
                              <img src={prod.images[0]} alt="" className="w-20 h-20 rounded-xl object-cover mx-auto" />
                              <button
                                onClick={() => toggleCompare(prod.id)}
                                className="absolute -top-1 -right-1 bg-stone-900 text-white rounded-full p-1 hover:bg-rose-600"
                              >
                                <X className="w-3 h-3" />
                              </button>
                            </div>
                            <span className="font-bold text-stone-950 block text-xs">{prod.name}</span>
                            <span className="text-sm font-black text-stone-900 mt-1 block">
                              ₹{prod.price.toLocaleString('en-IN')}
                            </span>
                            <button
                              disabled={prod.stock <= 0}
                              onClick={() => {
                                addToCart(prod, 1, '', '', true);
                                setIsCompareModalOpen(false);
                              }}
                              className="mt-2 w-full py-1.5 bg-stone-950 text-[#D4AF37] text-[10px] font-bold uppercase rounded-lg"
                            >
                              Add to Bag
                            </button>
                          </th>
                        );
                      })}
                    </tr>
                  </thead>
                  <tbody className="divide-y divide-stone-100">
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Material & Build</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-stone-800">{prod?.material || 'Full Grain Leather'}</td>;
                      })}
                    </tr>
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Weight</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-stone-800">{prod?.weight || '650g'}</td>;
                      })}
                    </tr>
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Laptop / Tech Fit</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-stone-800">{prod?.laptopCompatibility || '11" Tablet'}</td>;
                      })}
                    </tr>
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Dimensions</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-stone-800">{prod?.dimensions || 'Standard'}</td>;
                      })}
                    </tr>
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Strap & Carry</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-stone-800">{prod?.strapType || 'Adjustable Strap'}</td>;
                      })}
                    </tr>
                    <tr>
                      <td className="p-3 font-semibold text-stone-600">Warranty</td>
                      {compareList.map((id) => {
                        const prod = products.find((p) => p.id === id);
                        return <td key={id} className="p-3 text-center text-emerald-800 font-bold">{prod?.warranty || '1 Year'}</td>;
                      })}
                    </tr>
                  </tbody>
                </table>
              </div>
            )}
          </div>
        </div>
      )}

      {isCartOpen && (
        <div className="fixed inset-0 z-50 overflow-hidden">
          <div
            className="absolute inset-0 bg-stone-950/60 backdrop-blur-sm transition-opacity"
            onClick={() => setIsCartOpen(false)}
          />
          <div className="fixed inset-y-0 right-0 max-w-full flex pl-10">
            <div className="w-screen max-w-md bg-white shadow-2xl flex flex-col">
              <div className="p-5 border-b border-stone-200 flex items-center justify-between bg-stone-50">
                <div className="flex items-center gap-2">
                  <ShoppingBag className="w-5 h-5 text-stone-900" />
                  <h2 className="text-base font-serif font-bold text-stone-950">Your Shopping Bag</h2>
                  <span className="text-xs bg-stone-200 text-stone-800 px-2 py-0.5 rounded-full font-bold">
                    {cart.reduce((t, i) => t + i.quantity, 0)}
                  </span>
                </div>
                <button onClick={() => setIsCartOpen(false)} className="p-1 text-stone-400 hover:text-stone-700">
                  <X className="w-6 h-6" />
                </button>
              </div>

              {/* Items List */}
              <div className="flex-1 overflow-y-auto p-5 space-y-4">
                {cart.length === 0 ? (
                  <div className="h-full flex flex-col items-center justify-center text-center py-12">
                    <div className="w-16 h-16 rounded-full bg-stone-100 flex items-center justify-center text-stone-400 mb-3">
                      <ShoppingBag className="w-8 h-8" />
                    </div>
                    <h3 className="text-base font-serif font-semibold text-stone-800">Your bag is empty</h3>
                    <p className="text-xs text-stone-500 mt-1 max-w-xs">
                      Discover handcrafted Italian leather satchels, executive briefcases and sling bags.
                    </p>
                    <button
                      onClick={() => {
                        setIsCartOpen(false);
                        setCurrentPage('shop');
                      }}
                      className="mt-5 px-6 py-2.5 bg-stone-950 text-[#D4AF37] text-xs font-bold rounded-full uppercase tracking-wider hover:bg-stone-800"
                    >
                      Browse Catalog
                    </button>
                  </div>
                ) : (
                  cart.map((item, index) => {
                    const currentProduct = products.find((p) => p.id === item.id);
                    const liveStock = currentProduct ? currentProduct.stock : item.stock;

                    return (
                      <div key={`${item.id}-${index}`} className="flex gap-3 p-3 bg-stone-50 border border-stone-200 rounded-xl relative">
                        <img
                          src={item.images && item.images[0] ? item.images[0] : ''}
                          alt={item.name}
                          className="w-20 h-24 object-cover rounded-lg bg-stone-200 shrink-0"
                        />
                        <div className="flex-1 min-w-0 flex flex-col justify-between">
                          <div>
                            <div className="flex justify-between items-start">
                              <h4 className="text-xs font-bold text-stone-900 truncate">{item.name}</h4>
                              <button onClick={() => removeCartItem(index)} className="text-stone-400 hover:text-rose-600">
                                <Trash2 className="w-3.5 h-3.5" />
                              </button>
                            </div>
                            <p className="text-[11px] text-stone-500 mt-0.5">
                              {item.selectedColor} • {item.selectedSize}
                            </p>
                            <div className="flex items-center gap-2 mt-1">
                              <span className="text-xs font-bold text-stone-900">₹{item.price.toLocaleString('en-IN')}</span>
                              {item.mrp && (
                                <span className="text-[10px] text-stone-400 line-through">
                                  ₹{item.mrp.toLocaleString('en-IN')}
                                </span>
                              )}
                            </div>
                          </div>

                          <div className="flex items-center justify-between pt-2 border-t border-stone-200 mt-2">
                            <div className="flex items-center border border-stone-300 rounded-lg bg-white overflow-hidden">
                              <button onClick={() => updateCartQuantity(index, item.quantity - 1)} className="p-1 hover:bg-stone-100 text-stone-600">
                                <Minus className="w-3 h-3" />
                              </button>
                              <span className="px-2 text-xs font-bold text-stone-800">{item.quantity}</span>
                              <button
                                onClick={() => updateCartQuantity(index, item.quantity + 1)}
                                disabled={item.quantity >= liveStock}
                                className={`p-1 hover:bg-stone-100 text-stone-600 ${item.quantity >= liveStock ? 'opacity-40 cursor-not-allowed' : ''}`}
                              >
                                <Plus className="w-3 h-3" />
                              </button>
                            </div>
                            <span className="text-[10px] font-semibold text-emerald-700">
                              {liveStock <= 4 ? `Only ${liveStock} left` : 'In Ready Stock'}
                            </span>
                          </div>
                        </div>
                      </div>
                    );
                  })
                )}
              </div>

              {/* Cart Footer */}
              {cart.length > 0 && (
                <div className="p-5 border-t border-stone-200 bg-stone-50 space-y-3 max-h-[50vh] overflow-y-auto">
                  {/* Monogram / Name Personalization Section */}
                  <div className="p-3 rounded-xl bg-stone-100 border border-stone-300 space-y-2">
                    <label className="flex items-center justify-between cursor-pointer text-xs font-bold text-stone-900">
                      <span className="flex items-center gap-1.5">
                        <Type className="w-3.5 h-3.5 text-[#C5A059]" /> Add Bespoke Name Monogram (+₹149)
                      </span>
                      <input
                        type="checkbox"
                        checked={monogramConfig.enabled}
                        onChange={(e) => setMonogramConfig({ ...monogramConfig, enabled: e.target.checked })}
                        className="rounded accent-[#D4AF37] w-4 h-4 cursor-pointer"
                      />
                    </label>

                    {monogramConfig.enabled && (
                      <div className="space-y-2 pt-1 border-t border-stone-200">
                        <div className="flex gap-2">
                          <input
                            type="text"
                            maxLength={8}
                            placeholder="Initials / Name (e.g. S.A.)"
                            value={monogramConfig.text}
                            onChange={(e) => setMonogramConfig({ ...monogramConfig, text: e.target.value.toUpperCase() })}
                            className="flex-1 px-2.5 py-1.5 text-xs rounded-lg border border-stone-300 bg-white font-serif tracking-widest uppercase focus:outline-none"
                          />
                          <select
                            value={monogramConfig.style}
                            onChange={(e) => setMonogramConfig({ ...monogramConfig, style: e.target.value })}
                            className="px-2 py-1.5 text-xs rounded-lg border border-stone-300 bg-white font-medium"
                          >
                            <option value="Gold Foil">24K Gold Foil</option>
                            <option value="Silver Shimmer">Silver Chrome</option>
                            <option value="Blind Embossed">Blind Debossed</option>
                          </select>
                        </div>
                        {monogramConfig.text && (
                          <div className="text-[10px] text-center p-1.5 bg-stone-900 text-[#D4AF37] rounded-md font-serif tracking-widest uppercase shadow-inner">
                            Preview: [ {monogramConfig.text} • {monogramConfig.style} ]
                          </div>
                        )}
                      </div>
                    )}
                  </div>

                  {/* Azlan VIP Loyalty Coins Redemption */}
                  <div className="p-3 rounded-xl bg-amber-50/80 border border-amber-200/90 flex items-center justify-between text-xs">
                    <div>
                      <span className="font-bold text-amber-950 flex items-center gap-1">
                        <Coins className="w-3.5 h-3.5 text-[#D4AF37]" /> Redeem VIP Coins
                      </span>
                      <p className="text-[10px] text-amber-800">
                        Available Balance: <strong>{userCoins} Coins</strong> (₹{userCoins})
                      </p>
                    </div>
                    <button
                      onClick={handleApplyCoins}
                      className={`px-3 py-1.5 rounded-lg text-xs font-bold transition ${
                        coinsApplied > 0 ? 'bg-rose-700 text-white' : 'bg-stone-950 text-[#D4AF37]'
                      }`}
                    >
                      {coinsApplied > 0 ? 'Remove Coins' : `Apply ₹${Math.min(userCoins, cartSubtotal)}`}
                    </button>
                  </div>

                  {/* Luxury Gift Packaging */}
                  <div className="p-3 rounded-xl bg-white border border-stone-200 space-y-2">
                    <label className="flex items-start gap-2.5 cursor-pointer text-xs font-semibold text-stone-900">
                      <input
                        type="checkbox"
                        checked={isGiftWrapAdded}
                        onChange={(e) => setIsGiftWrapAdded(e.target.checked)}
                        className="mt-0.5 rounded accent-[#D4AF37] w-4 h-4 cursor-pointer"
                      />
                      <div>
                        <span className="flex items-center gap-1.5">
                          <Gift className="w-3.5 h-3.5 text-[#C5A059]" /> Add Luxury Gift Wrap & Greeting Card (+₹49)
                        </span>
                        <p className="text-[10px] font-normal text-stone-500">
                          Hand-tied satin ribbon, velvet pouch, and custom note.
                        </p>
                      </div>
                    </label>

                    {isGiftWrapAdded && (
                      <input
                        type="text"
                        placeholder="Type personalized message for greeting card..."
                        value={giftCardMessage}
                        onChange={(e) => setGiftCardMessage(e.target.value)}
                        className="w-full text-xs px-2.5 py-1.5 rounded-lg border border-stone-300 bg-white focus:outline-none"
                      />
                    )}
                  </div>

                  {/* Coupon Engine */}
                  <div className="bg-white p-2.5 rounded-xl border border-stone-200 shadow-xs">
                    {appliedCoupon ? (
                      <div className="flex items-center justify-between text-xs text-emerald-800 bg-emerald-50 px-2.5 py-1.5 rounded-lg border border-emerald-200">
                        <div className="flex items-center gap-1.5">
                          <Tag className="w-3.5 h-3.5" />
                          <span>
                            <strong>{appliedCoupon.code}</strong> applied (-₹{couponDiscount})
                          </span>
                        </div>
                        <button onClick={removeCoupon} className="text-stone-400 hover:text-rose-600">
                          <X className="w-3.5 h-3.5" />
                        </button>
                      </div>
                    ) : (
                      <div className="flex gap-2">
                        <input
                          type="text"
                          placeholder="Promo code (e.g. AZLAN10)"
                          value={couponInput}
                          onChange={(e) => setCouponInput(e.target.value.toUpperCase())}
                          className="flex-1 px-2.5 py-1.5 text-xs rounded-lg border border-stone-300 focus:outline-none uppercase"
                        />
                        <button
                          onClick={() => handleApplyCoupon()}
                          className="px-3 py-1.5 bg-stone-900 text-[#D4AF37] font-bold text-xs rounded-lg uppercase"
                        >
                          Apply
                        </button>
                      </div>
                    )}
                  </div>

                  {/* Financial Bill Details */}
                  <div className="space-y-1 text-xs">
                    <div className="flex justify-between text-stone-500">
                      <span>Bag Total</span>
                      <span>₹{cartSubtotal.toLocaleString('en-IN')}</span>
                    </div>
                    {monogramConfig.enabled && monogramConfig.text && (
                      <div className="flex justify-between text-stone-800">
                        <span>Bespoke Monogram Service</span>
                        <span>+₹149</span>
                      </div>
                    )}
                    {isGiftWrapAdded && (
                      <div className="flex justify-between text-amber-900">
                        <span>Luxury Gift Packaging</span>
                        <span>+₹49</span>
                      </div>
                    )}
                    {couponDiscount > 0 && (
                      <div className="flex justify-between text-emerald-700 font-semibold">
                        <span>Coupon Savings</span>
                        <span>-₹{couponDiscount.toLocaleString('en-IN')}</span>
                      </div>
                    )}
                    {coinsApplied > 0 && (
                      <div className="flex justify-between text-amber-700 font-semibold">
                        <span>VIP Coins Redeemed</span>
                        <span>-₹{coinsApplied.toLocaleString('en-IN')}</span>
                      </div>
                    )}
                    <div className="flex justify-between text-stone-500">
                      <span>Shipping</span>
                      <span className="text-emerald-700 font-bold">FREE ALL-INDIA</span>
                    </div>
                    <div className="flex justify-between text-sm font-bold text-stone-950 pt-2 border-t border-stone-200">
                      <span>Total Payable</span>
                      <span>₹{finalPayable.toLocaleString('en-IN')}</span>
                    </div>
                  </div>

                  <div className="pt-2 flex flex-col gap-2">
                    <button
                      onClick={() => {
                        setIsCartOpen(false);
                        setIsCheckoutOpen(true);
                      }}
                      className="w-full py-3 bg-stone-950 hover:bg-stone-900 text-[#D4AF37] font-bold text-xs uppercase tracking-widest rounded-xl shadow-lg transition flex items-center justify-center gap-2"
                    >
                      Proceed to Checkout <ArrowRight className="w-4 h-4" />
                    </button>
                    <button
                      onClick={() => handleWhatsAppOrder()}
                      className="w-full py-2 bg-emerald-700 hover:bg-emerald-800 text-white font-semibold text-xs rounded-xl flex items-center justify-center gap-2"
                    >
                      <MessageCircle className="w-4 h-4" /> Direct Order via WhatsApp
                    </button>
                  </div>
                </div>
              )}
            </div>
          </div>
        </div>
      )}

      {isWishlistOpen && (
        <div className="fixed inset-0 z-50 overflow-hidden">
          <div
            className="absolute inset-0 bg-stone-950/60 backdrop-blur-sm transition-opacity"
            onClick={() => setIsWishlistOpen(false)}
          />
          <div className="fixed inset-y-0 right-0 max-w-full flex pl-10">
            <div className="w-screen max-w-md bg-white shadow-2xl flex flex-col">
              <div className="p-5 border-b border-stone-200 flex items-center justify-between bg-stone-50">
                <div className="flex items-center gap-2">
                  <Heart className="w-5 h-5 text-rose-600 fill-current" />
                  <h2 className="text-base font-serif font-bold text-stone-950">Saved Wishlist</h2>
                  <span className="text-xs bg-rose-100 text-rose-800 px-2 py-0.5 rounded-full font-bold">
                    {wishlist.length}
                  </span>
                </div>
                <button onClick={() => setIsWishlistOpen(false)} className="p-1 text-stone-400 hover:text-stone-700">
                  <X className="w-6 h-6" />
                </button>
              </div>

              <div className="flex-1 overflow-y-auto p-5 space-y-4">
                {wishlist.length === 0 ? (
                  <div className="h-full flex flex-col items-center justify-center text-center py-12">
                    <Heart className="w-12 h-12 text-stone-300 mb-2 stroke-1" />
                    <h3 className="text-sm font-serif font-semibold text-stone-800">Your wishlist is empty</h3>
                    <p className="text-xs text-stone-500 mt-1 max-w-xs">
                      Tap the heart icon on any bag to save it here for later.
                    </p>
                  </div>
                ) : (
                  wishlist.map((prodId) => {
                    const prod = products.find((p) => p.id === prodId);
                    if (!prod) return null;
                    return (
                      <div key={prod.id} className="flex gap-3 p-3 bg-stone-50 border border-stone-200 rounded-xl relative">
                        <img
                          src={prod.images && prod.images[0] ? prod.images[0] : ''}
                          alt={prod.name}
                          className="w-16 h-20 object-cover rounded-lg bg-stone-200 shrink-0"
                        />
                        <div className="flex-1 min-w-0 flex flex-col justify-between">
                          <div>
                            <div className="flex justify-between items-start">
                              <h4 className="text-xs font-bold text-stone-900 truncate">{prod.name}</h4>
                              <button onClick={() => toggleWishlist(prod.id)} className="text-rose-500 hover:text-rose-700">
                                <Trash2 className="w-3.5 h-3.5" />
                              </button>
                            </div>
                            <span className="text-xs font-bold text-stone-900 block mt-1">
                              ₹{prod.price.toLocaleString('en-IN')}
                            </span>
                          </div>
                          <div className="flex items-center gap-2 mt-2">
                            <button
                              disabled={prod.stock <= 0}
                              onClick={() => {
                                addToCart(prod, 1, '', '', true);
                                setIsWishlistOpen(false);
                              }}
                              className={`flex-1 py-1.5 text-[11px] font-bold uppercase rounded-lg flex items-center justify-center gap-1 ${
                                prod.stock <= 0
                                  ? 'bg-stone-200 text-stone-400 cursor-not-allowed'
                                  : 'bg-stone-950 text-[#D4AF37] hover:bg-stone-800'
                              }`}
                            >
                              <ShoppingBag className="w-3.5 h-3.5" />
                              {prod.stock <= 0 ? 'Out of Stock' : 'Move to Bag'}
                            </button>
                          </div>
                        </div>
                      </div>
                    );
                  })
                )}
              </div>
            </div>
          </div>
        </div>
      )}

      {isTrackingModalOpen && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="relative bg-white rounded-3xl max-w-xl w-full shadow-2xl overflow-hidden border border-stone-200 animate-scale p-6 sm:p-8 space-y-6">
            <div className="flex justify-between items-start border-b border-stone-200 pb-4">
              <div className="flex items-center gap-2.5">
                <div className="w-10 h-10 rounded-2xl bg-emerald-100 text-emerald-800 flex items-center justify-center">
                  <Navigation className="w-5 h-5 text-emerald-700" />
                </div>
                <div>
                  <h3 className="text-lg font-serif font-bold text-stone-950">Azlan Express Tracking Portal</h3>
                  <p className="text-xs text-stone-500">Live Courier Dispatch & Delivery Timeline</p>
                </div>
              </div>
              <button onClick={() => setIsTrackingModalOpen(false)} className="text-stone-400 hover:text-stone-700">
                <X className="w-5 h-5" />
              </button>
            </div>

            <form
              onSubmit={(e) => {
                e.preventDefault();
                const q = trackingSearchQuery.trim().toUpperCase();
                const found = orders.find(
                  (o) => o.id.toUpperCase() === q || o.phone === q || (o.awbNumber && o.awbNumber.toUpperCase() === q)
                );
                if (found) {
                  setFoundTrackingOrder(found);
                  showToast(`Tracking status retrieved for ${found.id}`);
                } else {
                  setFoundTrackingOrder(null);
                  showToast('No record found matching this query.', 'error');
                }
              }}
              className="flex gap-2"
            >
              <input
                type="text"
                placeholder="Enter Order ID (e.g. AZL-89104) or Phone"
                value={trackingSearchQuery}
                onChange={(e) => setTrackingSearchQuery(e.target.value)}
                className="flex-1 px-3.5 py-2.5 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
              />
              <button
                type="submit"
                className="px-5 py-2.5 bg-stone-950 text-[#D4AF37] font-bold text-xs uppercase rounded-xl hover:bg-stone-900 transition"
              >
                Track Now
              </button>
            </form>

            {foundTrackingOrder ? (
              <div className="space-y-5 bg-stone-50 p-4 rounded-2xl border border-stone-200 text-xs">
                <div className="flex justify-between items-center pb-3 border-b border-stone-200">
                  <div>
                    <span className="font-bold text-stone-950 block text-sm">Order #{foundTrackingOrder.id}</span>
                    <span className="text-[11px] text-stone-500">
                      Courier: <strong>{foundTrackingOrder.courierPartner || 'Delhivery Express'}</strong>
                    </span>
                  </div>
                  <div className="text-right">
                    <span className="px-2.5 py-1 rounded-full text-[10px] font-bold uppercase bg-emerald-100 text-emerald-800">
                      {foundTrackingOrder.status}
                    </span>
                    <span className="text-[10px] text-stone-400 block mt-1">
                      AWB: <strong>{foundTrackingOrder.awbNumber || 'PENDING'}</strong>
                    </span>
                  </div>
                </div>

                <div className="space-y-4 relative pl-4 before:absolute before:left-6 before:top-2 before:bottom-2 before:w-0.5 before:bg-stone-300">
                  {(foundTrackingOrder.trackingTimeline || []).map((step, idx) => (
                    <div key={idx} className="relative flex items-start gap-4">
                      <div
                        className={`w-5 h-5 rounded-full flex items-center justify-center text-[10px] shrink-0 font-bold z-10 ${
                          step.completed
                            ? 'bg-emerald-600 text-white ring-4 ring-emerald-100'
                            : 'bg-stone-200 text-stone-500'
                        }`}
                      >
                        {step.completed ? <Check className="w-3 h-3" /> : idx + 1}
                      </div>
                      <div className="flex-1">
                        <div className="flex justify-between items-baseline">
                          <span className={`font-bold ${step.completed ? 'text-stone-900' : 'text-stone-400'}`}>
                            {step.stage}
                          </span>
                          <span className="text-[10px] text-stone-400">{step.time}</span>
                        </div>
                        <p className="text-[11px] text-stone-500 mt-0.5">{step.detail}</p>
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            ) : (
              <div className="text-center py-6 text-stone-500 text-xs">
                <Radio className="w-8 h-8 text-stone-300 mx-auto mb-2" />
                <p>Enter your 6-digit Order ID (like <strong>AZL-89104</strong>) to view exact dispatch status.</p>
              </div>
            )}
          </div>
        </div>
      )}

      {isWheelModalOpen && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/75 backdrop-blur-sm flex items-center justify-center p-4">
          <div className="relative bg-white rounded-3xl max-w-md w-full shadow-2xl overflow-hidden border border-stone-200 text-center p-6 space-y-4 animate-scale">
            <button
              onClick={() => setIsWheelModalOpen(false)}
              className="absolute top-4 right-4 z-20 w-8 h-8 rounded-full bg-stone-100 hover:bg-stone-200 text-stone-700 flex items-center justify-center"
            >
              <X className="w-4 h-4" />
            </button>

            <div>
              <span className="text-[10px] font-bold uppercase tracking-widest text-[#C5A059] bg-[#FAF8F5] px-2.5 py-1 rounded-full border border-[#D4AF37]/30">
                Azlan Exclusive Privileges
              </span>
              <h3 className="text-xl font-serif font-black text-stone-950 mt-1">Spin the Lucky Bag Wheel!</h3>
              <p className="text-xs text-stone-500 mt-1">
                Spin to win instant discount codes up to 15% OFF applied immediately at checkout.
              </p>
            </div>

            <div className="relative w-64 h-64 mx-auto my-4 flex items-center justify-center">
              <div className="absolute top-0 z-20 w-0 h-0 border-l-[12px] border-l-transparent border-r-[12px] border-r-transparent border-t-[24px] border-t-rose-600 drop-shadow-md"></div>
              <div
                style={{
                  transform: `rotate(${wheelRotation}deg)`,
                  transition: isSpinning ? 'transform 4.5s cubic-bezier(0.17, 0.67, 0.12, 0.99)' : 'none'
                }}
                className="w-full h-full rounded-full border-4 border-[#D4AF37] shadow-xl overflow-hidden relative"
              >
                <svg viewBox="0 0 100 100" className="w-full h-full">
                  {WHEEL_PRIZES.map((prize, idx) => {
                    const angle = 360 / WHEEL_PRIZES.length;
                    const startAngle = idx * angle;
                    const endAngle = (idx + 1) * angle;
                    const x1 = 50 + 50 * Math.cos((Math.PI * (startAngle - 90)) / 180);
                    const y1 = 50 + 50 * Math.sin((Math.PI * (startAngle - 90)) / 180);
                    const x2 = 50 + 50 * Math.cos((Math.PI * (endAngle - 90)) / 180);
                    const y2 = 50 + 50 * Math.sin((Math.PI * (endAngle - 90)) / 180);
                    const pathData = `M 50 50 L ${x1} ${y1} A 50 50 0 0 1 ${x2} ${y2} Z`;

                    const textAngle = startAngle + angle / 2;
                    const tx = 50 + 32 * Math.cos((Math.PI * (textAngle - 90)) / 180);
                    const ty = 50 + 32 * Math.sin((Math.PI * (textAngle - 90)) / 180);

                    return (
                      <g key={idx}>
                        <path d={pathData} fill={prize.color} />
                        <text
                          x={tx}
                          y={ty}
                          fill={prize.textColor}
                          fontSize="5.5"
                          fontWeight="bold"
                          textAnchor="middle"
                          dominantBaseline="central"
                          transform={`rotate(${textAngle}, ${tx}, ${ty})`}
                        >
                          {prize.text}
                        </text>
                      </g>
                    );
                  })}
                </svg>
                <div className="absolute inset-0 m-auto w-12 h-12 rounded-full bg-stone-950 border-2 border-[#D4AF37] text-[#D4AF37] flex items-center justify-center font-serif font-black text-sm shadow-lg">
                  AZ
                </div>
              </div>
            </div>

            {wonPrize && (
              <div className="p-3 bg-emerald-50 border border-emerald-200 rounded-2xl text-xs text-emerald-950 space-y-1">
                <span className="font-bold block text-sm">🎉 You won: {wonPrize.text}!</span>
                <p className="text-[11px]">
                  Promo code <strong className="text-emerald-800 underline">{wonPrize.code}</strong> has been auto-applied.
                </p>
              </div>
            )}

            <button
              disabled={isSpinning}
              onClick={handleSpinTheWheel}
              className={`w-full py-3 rounded-xl font-bold text-xs uppercase tracking-widest shadow-xl transition ${
                isSpinning ? 'bg-stone-300 text-stone-500 cursor-not-allowed' : 'bg-stone-950 hover:bg-stone-900 text-[#D4AF37]'
              }`}
            >
              {isSpinning ? 'Wheel is Spinning...' : 'Spin the Wheel for Free'}
            </button>
          </div>
        </div>
      )}

      {activeModalProduct && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="relative bg-white rounded-3xl max-w-4xl w-full shadow-2xl overflow-hidden border border-stone-200 animate-scale">
            <button
              onClick={() => setActiveModalProduct(null)}
              className="absolute top-4 right-4 z-20 w-8 h-8 rounded-full bg-white/90 text-stone-800 hover:bg-stone-950 hover:text-white flex items-center justify-center shadow"
            >
              <X className="w-5 h-5" />
            </button>

            <div className="grid grid-cols-1 md:grid-cols-2 max-h-[85vh] overflow-y-auto">
              {/* Product Visual Gallery with Zoom */}
              <div className="p-6 bg-stone-50 flex flex-col justify-between border-b md:border-b-0 md:border-r border-stone-200">
                <div>
                  <div
                    className="relative aspect-square rounded-2xl overflow-hidden bg-stone-200 shadow-inner cursor-crosshair group"
                    onMouseMove={handleMouseMoveZoom}
                    onMouseLeave={handleMouseLeaveZoom}
                  >
                    <img
                      src={
                        activeModalProduct.images && activeModalProduct.images[quickViewImageIndex]
                          ? activeModalProduct.images[quickViewImageIndex]
                          : activeModalProduct.images[0]
                      }
                      alt={activeModalProduct.name}
                      className="w-full h-full object-cover transition-all"
                    />

                    {/* Monogram Overlay Simulation on Image */}
                    {monogramConfig.enabled && monogramConfig.text && (
                      <div className="absolute bottom-6 right-6 px-3 py-1 bg-black/60 rounded-md backdrop-blur-xs border border-[#D4AF37]/50 text-[#D4AF37] font-serif tracking-[0.2em] font-bold text-xs shadow-xl uppercase">
                        {monogramConfig.text}
                      </div>
                    )}

                    {/* Magnifier Zoom Lens */}
                    <div
                      style={{
                        ...zoomStyle,
                        backgroundImage: `url(${
                          activeModalProduct.images && activeModalProduct.images[quickViewImageIndex]
                            ? activeModalProduct.images[quickViewImageIndex]
                            : activeModalProduct.images[0]
                        })`,
                        backgroundSize: '220%'
                      }}
                      className="absolute inset-0 pointer-events-none rounded-2xl border-2 border-[#D4AF37] hidden md:block"
                    />

                    {/* Live Viewers Badge */}
                    <div className="absolute top-3 left-3 bg-stone-950/80 text-amber-300 text-[10px] font-bold px-2.5 py-1 rounded-full backdrop-blur-xs flex items-center gap-1.5 shadow">
                      <Flame className="w-3.5 h-3.5 text-orange-500 fill-current" />
                      <span>{activeModalProduct.liveViewers || 12} people viewing now</span>
                    </div>

                    {activeModalProduct.stock <= 0 && (
                      <div className="absolute inset-0 bg-stone-950/60 backdrop-blur-xs flex items-center justify-center">
                        <span className="px-4 py-2 bg-rose-600 text-white text-xs font-bold uppercase tracking-wider rounded-md">
                          Sold Out
                        </span>
                      </div>
                    )}
                  </div>

                  {activeModalProduct.images && activeModalProduct.images.length > 1 && (
                    <div className="flex gap-2 overflow-x-auto pt-3">
                      {activeModalProduct.images.map((img, idx) => (
                        <button
                          key={idx}
                          onClick={() => setQuickViewImageIndex(idx)}
                          className={`w-14 h-14 rounded-xl overflow-hidden border-2 shrink-0 transition ${
                            quickViewImageIndex === idx ? 'border-[#D4AF37] ring-1 ring-[#D4AF37]' : 'border-stone-200 opacity-70 hover:opacity-100'
                          }`}
                        >
                          <img src={img} alt="" className="w-full h-full object-cover" />
                        </button>
                      ))}
                    </div>
                  )}
                </div>

                {/* Delivery Pincode Checker */}
                <div className="mt-6 pt-4 border-t border-stone-200">
                  <span className="text-[11px] font-bold uppercase text-stone-700 block mb-1.5 flex items-center gap-1">
                    <MapPin className="w-3.5 h-3.5 text-[#C5A059]" /> Check Delivery & COD Availability
                  </span>
                  <div className="flex gap-2">
                    <input
                      type="text"
                      maxLength={6}
                      placeholder="Enter 6-digit PIN"
                      value={pincodeQuery}
                      onChange={(e) => setPincodeQuery(e.target.value.replace(/\D/g, ''))}
                      className="w-36 px-2.5 py-1.5 text-xs rounded-lg border border-stone-300 focus:outline-none"
                    />
                    <button
                      onClick={checkDeliveryPincode}
                      className="px-3 py-1.5 bg-stone-900 text-white text-xs font-semibold rounded-lg hover:bg-stone-800"
                    >
                      Check PIN
                    </button>
                  </div>

                  {pincodeResult && (
                    <div className="mt-2.5 p-2.5 bg-emerald-50 border border-emerald-200 rounded-xl text-[11px] text-emerald-900 space-y-0.5">
                      <div className="font-bold flex items-center gap-1">
                        <CheckCircle className="w-3.5 h-3.5 text-emerald-600" /> Delivery Available for {pincodeResult.pincode}
                      </div>
                      <p>Estimated Express Delivery in <strong>{pincodeResult.deliveryDays} Business Days</strong>.</p>
                      <p className="text-emerald-700">Cash on Delivery (COD) & Free Shipping Eligible.</p>
                    </div>
                  )}
                </div>
              </div>

              {/* Product Specifications & Monogram Personalizer */}
              <div className="p-6 md:p-8 flex flex-col justify-between space-y-6">
                <div>
                  <div className="flex items-center justify-between gap-2">
                    <span className="text-[10px] font-bold uppercase tracking-widest text-[#C5A059] bg-[#FAF8F5] px-2.5 py-1 rounded-md border border-[#D4AF37]/30">
                      {activeModalProduct.category}
                    </span>
                    <div className="flex items-center gap-2">
                      <button
                        onClick={() => toggleCompare(activeModalProduct.id)}
                        className={`text-xs px-2.5 py-1 rounded-lg border flex items-center gap-1 ${
                          compareList.includes(activeModalProduct.id)
                            ? 'bg-stone-900 text-[#D4AF37] border-stone-900'
                            : 'bg-white text-stone-700 border-stone-300'
                        }`}
                      >
                        <Scale className="w-3 h-3" /> Compare
                      </button>
                      <button
                        onClick={() => toggleWishlist(activeModalProduct.id)}
                        className="p-1.5 rounded-full hover:bg-stone-100 text-stone-600 transition"
                      >
                        <Heart
                          className={`w-5 h-5 ${wishlist.includes(activeModalProduct.id) ? 'text-rose-600 fill-current' : ''}`}
                        />
                      </button>
                    </div>
                  </div>

                  <h3 className="text-xl font-serif font-bold text-stone-950 mt-2">
                    {activeModalProduct.name}
                  </h3>

                  <div className="flex items-center gap-2 mt-1 text-xs">
                    <div className="flex items-center text-amber-500 font-bold">
                      <Star className="w-3.5 h-3.5 fill-current" />
                      <span className="ml-1">{activeModalProduct.rating}</span>
                    </div>
                    <span className="text-stone-400">|</span>
                    <span className="text-stone-500">{activeModalProduct.reviewsCount} Verified Buyer Reviews</span>
                  </div>

                  {/* Pricing */}
                  <div className="flex items-baseline gap-3 mt-3">
                    <span className="text-2xl font-black text-stone-950">
                      ₹{activeModalProduct.price.toLocaleString('en-IN')}
                    </span>
                    <span className="text-sm text-stone-400 line-through">
                      ₹{activeModalProduct.mrp.toLocaleString('en-IN')}
                    </span>
                    <span className="text-xs font-bold text-emerald-700 bg-emerald-50 px-2 py-0.5 rounded">
                      {Math.round(((activeModalProduct.mrp - activeModalProduct.price) / activeModalProduct.mrp) * 100)}% OFF
                    </span>
                  </div>

                  {/* Live Stock Counter */}
                  <div className="mt-3">
                    {activeModalProduct.stock > 0 ? (
                      <span className="inline-flex items-center gap-1.5 text-xs font-semibold text-emerald-800 bg-emerald-50 px-2.5 py-1 rounded-full">
                        <span className="w-2 h-2 rounded-full bg-emerald-600 animate-ping"></span>
                        {activeModalProduct.stock <= (activeModalProduct.lowStockThreshold || 4)
                          ? `Hurry! Only ${activeModalProduct.stock} left in stock`
                          : `${activeModalProduct.stock} units in ready stock`}
                      </span>
                    ) : (
                      <span className="inline-flex items-center gap-1 text-xs font-semibold text-rose-700 bg-rose-50 px-2.5 py-1 rounded-full">
                        <AlertTriangle className="w-3.5 h-3.5" /> Out of stock - Next batch restocking soon
                      </span>
                    )}
                  </div>

                  {/* Monogram Live Personalization Box */}
                  <div className="mt-4 p-3 bg-stone-100/80 rounded-2xl border border-stone-300 space-y-2">
                    <div className="flex justify-between items-center text-xs font-bold text-stone-900">
                      <span className="flex items-center gap-1.5">
                        <Type className="w-3.5 h-3.5 text-[#C5A059]" /> Engrave Initials / Name (+₹149)
                      </span>
                      <input
                        type="checkbox"
                        checked={monogramConfig.enabled}
                        onChange={(e) => setMonogramConfig({ ...monogramConfig, enabled: e.target.checked })}
                        className="rounded accent-stone-950 w-4 h-4 cursor-pointer"
                      />
                    </div>
                    {monogramConfig.enabled && (
                      <div className="space-y-2 pt-1">
                        <input
                          type="text"
                          maxLength={8}
                          placeholder="Your Initials (e.g. S.A.)"
                          value={monogramConfig.text}
                          onChange={(e) => setMonogramConfig({ ...monogramConfig, text: e.target.value.toUpperCase() })}
                          className="w-full text-xs px-2.5 py-1.5 rounded-lg border border-stone-300 bg-white uppercase font-serif tracking-widest"
                        />
                        <div className="flex gap-2">
                          {['Gold Foil', 'Silver Shimmer', 'Blind Embossed'].map((style) => (
                            <button
                              key={style}
                              type="button"
                              onClick={() => setMonogramConfig({ ...monogramConfig, style })}
                              className={`flex-1 py-1 text-[10px] font-bold rounded-md border ${
                                monogramConfig.style === style ? 'bg-stone-950 text-[#D4AF37] border-stone-950' : 'bg-white text-stone-600'
                              }`}
                            >
                              {style}
                            </button>
                          ))}
                        </div>
                      </div>
                    )}
                  </div>

                  {/* Color Selector */}
                  {activeModalProduct.colors && activeModalProduct.colors.length > 0 && (
                    <div className="mt-4">
                      <label className="text-xs font-bold uppercase tracking-wider text-stone-600 block mb-1.5">
                        Selected Shade: <strong className="text-stone-950">{selectedVariantColor}</strong>
                      </label>
                      <div className="flex flex-wrap gap-2">
                        {activeModalProduct.colors.map((color) => (
                          <button
                            key={color}
                            onClick={() => setSelectedVariantColor(color)}
                            className={`px-3 py-1 text-xs rounded-lg border font-medium transition ${
                              selectedVariantColor === color
                                ? 'bg-stone-950 text-white border-stone-950'
                                : 'bg-white text-stone-700 border-stone-300 hover:border-stone-400'
                            }`}
                          >
                            {color}
                          </button>
                        ))}
                      </div>
                    </div>
                  )}

                  {/* Bag Capacity Visualizer */}
                  <div className="mt-4 p-3 bg-stone-50 rounded-2xl border border-stone-200">
                    <span className="text-[11px] font-bold uppercase text-stone-800 block mb-2 flex items-center gap-1.5">
                      <Package className="w-3.5 h-3.5 text-[#C5A059]" /> What Fits Inside This Bag?
                      <span className="text-[10px] text-stone-400 font-normal">
                        ({activeModalProduct.dimensions || 'Spacious Fit'})
                      </span>
                    </span>
                    <div className="grid grid-cols-2 gap-2 text-[11px] text-stone-700">
                      {(activeModalProduct.fitsInside || ['Smartphone', 'Cosmetics', 'Wallet', 'Keys']).map((item, idx) => (
                        <div key={idx} className="flex items-center gap-1.5 bg-white p-1.5 rounded-lg border border-stone-200/80">
                          <CheckCircle className="w-3 h-3 text-emerald-600 shrink-0" />
                          <span className="truncate">{item}</span>
                        </div>
                      ))}
                    </div>
                  </div>

                  <p className="text-xs leading-relaxed text-stone-600 mt-4">
                    {activeModalProduct.description}
                  </p>
                </div>

                {/* Actions */}
                <div className="pt-4 border-t border-stone-200 flex flex-col sm:flex-row gap-2.5">
                  <button
                    disabled={activeModalProduct.stock <= 0}
                    onClick={() => {
                      addToCart(activeModalProduct, 1, selectedVariantColor, selectedVariantSize, true);
                      setActiveModalProduct(null);
                    }}
                    className={`flex-1 py-3 px-4 rounded-xl text-xs font-bold uppercase tracking-widest flex items-center justify-center gap-2 transition ${
                      activeModalProduct.stock <= 0
                        ? 'bg-stone-300 text-stone-500 cursor-not-allowed'
                        : 'bg-stone-950 text-[#D4AF37] hover:bg-stone-900'
                    }`}
                  >
                    <ShoppingBag className="w-4 h-4" /> Add to Bag
                  </button>
                  <button
                    onClick={() => handleWhatsAppOrder(activeModalProduct)}
                    className="py-3 px-4 rounded-xl text-xs font-bold bg-emerald-700 hover:bg-emerald-800 text-white flex items-center justify-center gap-1.5 transition"
                  >
                    <MessageCircle className="w-4 h-4" /> Buy on WhatsApp
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      )}

      {}
      {isCheckoutOpen && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="relative bg-white rounded-3xl max-w-2xl w-full shadow-2xl overflow-hidden border border-stone-200 animate-scale">
            <div className="p-6 border-b border-stone-200 bg-stone-950 text-white flex justify-between items-center">
              <div>
                <h3 className="text-base sm:text-lg font-serif font-bold text-[#D4AF37]">Checkout & Shipping Address</h3>
                <p className="text-xs text-stone-400">Azlan Fashion Central Logistics Dispatches across India</p>
              </div>
              <button onClick={() => setIsCheckoutOpen(false)} className="text-stone-400 hover:text-white">
                <X className="w-5 h-5" />
              </button>
            </div>

            <form onSubmit={handlePlaceOrder} className="p-6 space-y-4 max-h-[80vh] overflow-y-auto">
              <div className="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div>
                  <label className="text-xs font-bold text-stone-700 block mb-1">Full Name *</label>
                  <input
                    required
                    type="text"
                    placeholder="e.g. Sajid Shaikh"
                    value={checkoutData.fullName}
                    onChange={(e) => setCheckoutData({ ...checkoutData, fullName: e.target.value })}
                    className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
                  />
                </div>
                <div>
                  <label className="text-xs font-bold text-stone-700 block mb-1">Mobile / WhatsApp Number *</label>
                  <input
                    required
                    type="tel"
                    placeholder="e.g. 7762067143"
                    value={checkoutData.mobile}
                    onChange={(e) => setCheckoutData({ ...checkoutData, mobile: e.target.value })}
                    className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
                  />
                </div>
              </div>

              <div>
                <label className="text-xs font-bold text-stone-700 block mb-1">Email Address</label>
                <input
                  type="email"
                  placeholder="e.g. workwithsajid@zohomail.in"
                  value={checkoutData.email}
                  onChange={(e) => setCheckoutData({ ...checkoutData, email: e.target.value })}
                  className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
                />
              </div>

              <div>
                <label className="text-xs font-bold text-stone-700 block mb-1">Street Address *</label>
                <textarea
                  required
                  rows={2}
                  placeholder="Apartment, building name, landmark, street..."
                  value={checkoutData.address}
                  onChange={(e) => setCheckoutData({ ...checkoutData, address: e.target.value })}
                  className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
                />
              </div>

              <div className="grid grid-cols-3 gap-3">
                <div>
                  <label className="text-xs font-bold text-stone-700 block mb-1">City</label>
                  <input
                    type="text"
                    placeholder="City"
                    value={checkoutData.city}
                    onChange={(e) => setCheckoutData({ ...checkoutData, city: e.target.value })}
                    className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300"
                  />
                </div>
                <div>
                  <label className="text-xs font-bold text-stone-700 block mb-1">State</label>
                  <input
                    type="text"
                    value={checkoutData.state}
                    onChange={(e) => setCheckoutData({ ...checkoutData, state: e.target.value })}
                    className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300"
                  />
                </div>
                <div>
                  <label className="text-xs font-bold text-stone-700 block mb-1">Pincode *</label>
                  <input
                    required
                    type="text"
                    maxLength={6}
                    placeholder="Pincode"
                    value={checkoutData.pincode}
                    onChange={(e) => setCheckoutData({ ...checkoutData, pincode: e.target.value.replace(/\D/g, '') })}
                    className="w-full px-3 py-2 text-xs rounded-xl border border-stone-300"
                  />
                </div>
              </div>

              {/* Payment Method Selector */}
              <div className="pt-2">
                <label className="text-xs font-bold text-stone-700 block mb-2">Select Payment Method</label>
                <div className="grid grid-cols-2 gap-3">
                  <div
                    onClick={() => setCheckoutData({ ...checkoutData, paymentMethod: 'UPI' })}
                    className={`p-3 rounded-xl border text-xs cursor-pointer flex items-center justify-between transition ${
                      checkoutData.paymentMethod === 'UPI' ? 'border-stone-900 bg-stone-50 font-bold' : 'border-stone-200'
                    }`}
                  >
                    <span>Instant UPI / Scan & Pay</span>
                    <QrCode className="w-4 h-4 text-emerald-600" />
                  </div>
                  <div
                    onClick={() => setCheckoutData({ ...checkoutData, paymentMethod: 'COD' })}
                    className={`p-3 rounded-xl border text-xs cursor-pointer flex items-center justify-between transition ${
                      checkoutData.paymentMethod === 'COD' ? 'border-stone-900 bg-stone-50 font-bold' : 'border-stone-200'
                    }`}
                  >
                    <span>Cash on Delivery (COD)</span>
                    <Truck className="w-4 h-4 text-stone-600" />
                  </div>
                </div>
              </div>

              {/* Dynamic UPI QR Display */}
              {checkoutData.paymentMethod === 'UPI' && (
                <div className="p-4 bg-emerald-50/70 border border-emerald-200 rounded-2xl flex flex-col sm:flex-row items-center gap-4">
                  <div className="p-2 bg-white rounded-xl shadow-xs border border-emerald-200 shrink-0">
                    <img
                      src={`https://api.qrserver.com/v1/create-qr-code/?size=130x130&data=upi://pay?pa=7762067143@upi&pn=Azlan%20Fashion&am=${finalPayable}&cu=INR`}
                      alt="UPI QR Code"
                      className="w-28 h-28"
                    />
                  </div>
                  <div className="space-y-1 text-xs text-stone-700 text-center sm:text-left">
                    <span className="font-bold text-emerald-950 block">Instant Scan & Pay with Any UPI App</span>
                    <p className="text-[11px] text-stone-600">
                      Scan with Google Pay, PhonePe, Paytm or BHIM to pay <strong>₹{finalPayable.toLocaleString('en-IN')}</strong> directly to <code>7762067143@upi</code>.
                    </p>
                    <p className="text-[10px] text-emerald-800 font-semibold">
                      Your order confirmation & GST bill generate immediately.
                    </p>
                  </div>
                </div>
              )}

              {/* Order Bill Summary */}
              <div className="p-3 bg-stone-50 rounded-xl text-xs space-y-1 border border-stone-200">
                <div className="flex justify-between font-bold text-stone-900 text-sm">
                  <span>Net Payable Amount:</span>
                  <span className="text-base font-black text-stone-950">₹{finalPayable.toLocaleString('en-IN')}</span>
                </div>
                <p className="text-[10px] text-stone-500">Live inventory locks in real time once confirmed.</p>
              </div>

              {/* Action Buttons */}
              <div className="pt-2 flex gap-3">
                <button
                  type="submit"
                  className="flex-1 py-3 bg-stone-950 hover:bg-stone-900 text-[#D4AF37] font-bold text-xs uppercase tracking-wider rounded-xl shadow-lg transition"
                >
                  Place Order Now
                </button>
                <button
                  type="button"
                  onClick={() => handleWhatsAppOrder()}
                  className="px-4 py-3 bg-emerald-700 hover:bg-emerald-800 text-white font-semibold text-xs rounded-xl flex items-center gap-1.5 transition"
                >
                  <MessageCircle className="w-4 h-4" /> Send on WhatsApp
                </button>
              </div>
            </form>
          </div>
        </div>
      )}

      {activeShippingLabelOrder && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="bg-white rounded-2xl max-w-lg w-full shadow-2xl overflow-hidden border border-stone-300 p-6 space-y-4 animate-scale">
            <div className="flex justify-between items-center border-b pb-3">
              <h3 className="text-sm font-serif font-bold text-stone-900 flex items-center gap-1.5">
                <Barcode className="w-4 h-4 text-stone-950" /> Courier Packaging Shipping Label
              </h3>
              <div className="flex gap-2">
                <button
                  onClick={() => window.print()}
                  className="p-1.5 rounded-lg bg-stone-100 hover:bg-stone-200 text-stone-800 text-xs font-bold flex items-center gap-1"
                >
                  <Printer className="w-3.5 h-3.5" /> Print Thermal Sticker
                </button>
                <button onClick={() => setActiveShippingLabelOrder(null)} className="p-1.5 text-stone-400 hover:text-stone-700">
                  <X className="w-4 h-4" />
                </button>
              </div>
            </div>

            <div className="border-2 border-dashed border-stone-800 p-4 rounded-xl font-mono text-xs space-y-3 bg-stone-50/50">
              <div className="flex justify-between items-start border-b border-stone-300 pb-2">
                <div>
                  <span className="text-base font-black tracking-widest uppercase block">AZLAN FASHION</span>
                  <span className="text-[10px] text-stone-500">Logistics Hub #B4, Central Cargo Complex</span>
                </div>
                <div className="text-right">
                  <span className="px-2 py-0.5 border border-stone-800 text-stone-950 font-bold uppercase text-[10px]">
                    {activeShippingLabelOrder.paymentMethod.includes('COD') ? 'COLLECT COD' : 'PREPAID EXPRESS'}
                  </span>
                  <p className="text-[10px] font-bold mt-1">₹{activeShippingLabelOrder.totalAmount}</p>
                </div>
              </div>

              <div className="text-center py-2 bg-white rounded border border-stone-200">
                <div className="tracking-[0.3em] font-black text-2xl text-stone-950 font-sans">
                  ||| | | |||| || | || |||| | ||
                </div>
                <span className="text-[10px] font-bold text-stone-600 block mt-1">
                  AWB: {activeShippingLabelOrder.awbNumber || 'DEL-BOM-89104'}
                </span>
              </div>

              <div className="space-y-1">
                <span className="text-[10px] font-bold text-stone-400 uppercase">DELIVER TO (CONSIGNEE):</span>
                <p className="text-xs font-bold text-stone-950">{activeShippingLabelOrder.customerName}</p>
                <p className="text-[11px] leading-tight text-stone-700">
                  {activeShippingLabelOrder.address}, {activeShippingLabelOrder.city}, {activeShippingLabelOrder.state} - <strong>{activeShippingLabelOrder.pincode}</strong>
                </p>
                <p className="text-[11px] font-bold text-stone-900 mt-1">Phone: {activeShippingLabelOrder.phone}</p>
              </div>

              <div className="border-t border-stone-300 pt-2 text-[10px] text-stone-600 flex justify-between">
                <span>Items: {activeShippingLabelOrder.items.length} units</span>
                <span>Order Ref: #{activeShippingLabelOrder.id}</span>
                <span>Date: {activeShippingLabelOrder.date.slice(0, 10)}</span>
              </div>
            </div>

            <button
              onClick={() => setActiveShippingLabelOrder(null)}
              className="w-full py-2 bg-stone-950 text-[#D4AF37] font-bold text-xs rounded-xl"
            >
              Done / Close Label
            </button>
          </div>
        </div>
      )}

      {activeInvoiceOrder && (
        <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-3 sm:p-4">
          <div className="bg-white rounded-3xl max-w-2xl w-full shadow-2xl overflow-hidden border border-stone-200 p-6 sm:p-8 space-y-6 animate-scale">
            <div className="flex justify-between items-start border-b border-stone-200 pb-4">
              <div>
                <div className="flex items-center gap-2">
                  <div className="w-8 h-8 rounded-full bg-stone-950 text-[#D4AF37] flex items-center justify-center font-serif font-bold text-sm">
                    A
                  </div>
                  <h3 className="text-lg font-serif font-bold text-stone-950">Azlan Fashion - Tax Invoice</h3>
                </div>
                <p className="text-xs text-stone-500 mt-1">Official E-Commerce Receipt & Delivery Pass</p>
              </div>
              <div className="flex gap-2">
                <button
                  onClick={() => window.print()}
                  className="p-2 rounded-xl bg-stone-100 hover:bg-stone-200 text-stone-700 text-xs font-semibold flex items-center gap-1.5"
                >
                  <Printer className="w-4 h-4" /> Print / PDF
                </button>
                <button onClick={() => setActiveInvoiceOrder(null)} className="p-2 rounded-xl text-stone-400 hover:text-stone-700">
                  <X className="w-5 h-5" />
                </button>
              </div>
            </div>

            <div className="grid grid-cols-2 gap-4 text-xs">
              <div>
                <span className="font-bold text-stone-400 uppercase text-[10px] block">Sold By</span>
                <p className="font-bold text-stone-900">Azlan Fashion India</p>
                <p className="text-stone-600">WhatsApp / Call: +91 7762067143</p>
                <p className="text-stone-600">Email: workwithsajid@zohomail.in</p>
                <p className="text-[10px] text-stone-400 mt-1">GSTIN: 27AABCA1234F1Z9 (Provisional)</p>
              </div>
              <div className="text-right">
                <span className="font-bold text-stone-400 uppercase text-[10px] block">Billed To</span>
                <p className="font-bold text-stone-900">{activeInvoiceOrder.customerName}</p>
                <p className="text-stone-600">{activeInvoiceOrder.address}, {activeInvoiceOrder.city}</p>
                <p className="text-stone-600">PIN: {activeInvoiceOrder.pincode} | Phone: {activeInvoiceOrder.phone}</p>
                <p className="text-stone-600 mt-1">Invoice ID: <strong>{activeInvoiceOrder.id}</strong></p>
              </div>
            </div>

            <div className="border border-stone-200 rounded-xl overflow-hidden">
              <table className="w-full text-xs text-left">
                <thead className="bg-stone-50 text-stone-600 border-b border-stone-200 font-bold uppercase text-[10px]">
                  <tr>
                    <th className="p-2.5">Item Description</th>
                    <th className="p-2.5">Qty</th>
                    <th className="p-2.5">Unit Price</th>
                    <th className="p-2.5 text-right">Total</th>
                  </tr>
                </thead>
                <tbody className="divide-y divide-stone-100">
                  {activeInvoiceOrder.items.map((it, idx) => (
                    <tr key={idx}>
                      <td className="p-2.5">
                        <span className="font-semibold text-stone-900">{it.name}</span>
                        {it.color && <span className="text-[10px] text-stone-500 block">Shade: {it.color}</span>}
                      </td>
                      <td className="p-2.5">{it.qty}</td>
                      <td className="p-2.5">₹{it.price.toLocaleString('en-IN')}</td>
                      <td className="p-2.5 text-right font-bold">₹{((it.price || 0) * (it.qty || 1)).toLocaleString('en-IN')}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>

            <div className="flex justify-between items-end text-xs">
              <div className="text-[11px] text-stone-500 space-y-0.5">
                <p>Payment Mode: <strong>{activeInvoiceOrder.paymentMethod}</strong></p>
                <p>Status: <span className="text-emerald-700 font-bold">{activeInvoiceOrder.status}</span></p>
                {activeInvoiceOrder.monogramDetails && (
                  <p className="text-stone-900 font-semibold">
                    🔤 Monogram: "{activeInvoiceOrder.monogramDetails.text}" ({activeInvoiceOrder.monogramDetails.style})
                  </p>
                )}
                {activeInvoiceOrder.coinsEarned > 0 && (
                  <p className="text-amber-800 font-semibold">🪙 Earned {activeInvoiceOrder.coinsEarned} Azlan Loyalty Coins</p>
                )}
              </div>
              <div className="space-y-1 text-right">
                {activeInvoiceOrder.discountAmount > 0 && (
                  <p className="text-emerald-700">Savings & Discounts: -₹{activeInvoiceOrder.discountAmount.toLocaleString('en-IN')}</p>
                )}
                {activeInvoiceOrder.giftWrapFee > 0 && (
                  <p className="text-amber-900">Gift Wrap: +₹{activeInvoiceOrder.giftWrapFee}</p>
                )}
                <p className="text-stone-500">Shipping: <strong>FREE</strong></p>
                <p className="text-base font-black text-stone-950">Grand Total: ₹{activeInvoiceOrder.totalAmount.toLocaleString('en-IN')}</p>
              </div>
            </div>

            <button
              onClick={() => setActiveInvoiceOrder(null)}
              className="w-full py-2.5 bg-stone-950 text-[#D4AF37] font-bold text-xs rounded-xl"
            >
              Close Invoice
            </button>
          </div>
        </div>
      )}

      {productFormOpen && (
        <ProductFormModal
          product={editingProduct}
          categories={categories}
          onClose={() => {
            setProductFormOpen(false);
            setEditingProduct(null);
          }}
          onSave={handleSaveProduct}
        />
      )}

      {}
      <footer className="bg-stone-950 text-stone-400 text-xs border-t border-stone-800">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-14">
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-10">
            {/* Brand Intro */}
            <div className="space-y-4">
              <div className="flex items-center gap-3">
                <div className="w-9 h-9 rounded-full bg-[#D4AF37] text-stone-950 flex items-center justify-center font-serif text-lg font-bold">
                  A
                </div>
                <div>
                  <span className="text-lg font-serif font-black tracking-widest uppercase text-white block">
                    Azlan Fashion
                  </span>
                  <span className="text-[9px] tracking-widest text-[#D4AF37] uppercase block">
                    Curated Luxury Handbags
                  </span>
                </div>
              </div>
              <p className="text-stone-400 text-xs leading-relaxed">
                Elevating Indian everyday elegance with timeless craftsmanship, durable materials,
                and exquisite bag silhouettes crafted for work, travel and celebration.
              </p>
              <div className="flex gap-3 text-stone-300">
                <a
                  href="https://wa.me/917762067143"
                  target="_blank"
                  rel="noreferrer"
                  className="w-8 h-8 rounded-full bg-stone-900 border border-stone-800 flex items-center justify-center hover:text-[#D4AF37] hover:border-[#D4AF37] transition"
                >
                  <MessageCircle className="w-4 h-4" />
                </a>
                <a
                  href="tel:7762067143"
                  className="w-8 h-8 rounded-full bg-stone-900 border border-stone-800 flex items-center justify-center hover:text-[#D4AF37] hover:border-[#D4AF37] transition"
                >
                  <Phone className="w-4 h-4" />
                </a>
                <a
                  href="mailto:workwithsajid@zohomail.in"
                  className="w-8 h-8 rounded-full bg-stone-900 border border-stone-800 flex items-center justify-center hover:text-[#D4AF37] hover:border-[#D4AF37] transition"
                >
                  <Mail className="w-4 h-4" />
                </a>
              </div>
            </div>

            {/* Quick Links */}
            <div>
              <h4 className="text-white font-serif font-bold text-sm tracking-wider uppercase mb-4 border-b border-stone-800 pb-2">
                Quick Navigation
              </h4>
              <ul className="space-y-2.5">
                <li>
                  <button onClick={() => { setCurrentPage('home'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Home Page
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('shop'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Shop Collection
                  </button>
                </li>
                <li>
                  <button onClick={() => setIsReelsModalOpen(true)} className="text-purple-400 hover:text-purple-300 font-semibold">
                    Reels Lookbook
                  </button>
                </li>
                <li>
                  <button
                    onClick={() => {
                      setFoundTrackingOrder(null);
                      setIsTrackingModalOpen(true);
                    }}
                    className="text-[#D4AF37] font-semibold hover:underline"
                  >
                    Track My Order
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('categories'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Browse Categories
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('about'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    About Our Brand
                  </button>
                </li>
              </ul>
            </div>

            {/* Policies */}
            <div>
              <h4 className="text-white font-serif font-bold text-sm tracking-wider uppercase mb-4 border-b border-stone-800 pb-2">
                Policies & Terms
              </h4>
              <ul className="space-y-2.5">
                <li>
                  <button onClick={() => { setCurrentPage('policies'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Privacy Policy
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('policies'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Terms & Conditions
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('policies'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Shipping Policy (All India)
                  </button>
                </li>
                <li>
                  <button onClick={() => { setCurrentPage('policies'); window.scrollTo({ top: 0, behavior: 'smooth' }); }} className="hover:text-[#D4AF37] transition">
                    Returns & Replacement
                  </button>
                </li>
                <li>
                  <button
                    onClick={() => { setCurrentPage(adminUser ? 'admin-dashboard' : 'admin-login'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
                    className="text-stone-500 hover:text-[#D4AF37] transition flex items-center gap-1"
                  >
                    <Lock className="w-3 h-3" /> Staff Protected Access
                  </button>
                </li>
              </ul>
            </div>

            {/* Concierge */}
            <div>
              <h4 className="text-white font-serif font-bold text-sm tracking-wider uppercase mb-4 border-b border-stone-800 pb-2">
                Azlan Concierge
              </h4>
              <div className="space-y-3">
                <div className="flex items-start gap-2.5">
                  <Phone className="w-4 h-4 text-[#D4AF37] shrink-0 mt-0.5" />
                  <div>
                    <span className="block text-white font-medium">+91 7762067143</span>
                    <span className="text-[11px] text-stone-500">Mon - Sat, 10 AM to 8 PM IST</span>
                  </div>
                </div>
                <div className="flex items-start gap-2.5">
                  <Mail className="w-4 h-4 text-[#D4AF37] shrink-0 mt-0.5" />
                  <div>
                    <span className="block text-white font-medium">workwithsajid@zohomail.in</span>
                    <span className="text-[11px] text-stone-500">Prompt responses within 2 hrs</span>
                  </div>
                </div>
                <div className="pt-2">
                  <a
                    href="https://wa.me/917762067143"
                    target="_blank"
                    rel="noreferrer"
                    className="inline-flex items-center gap-2 px-3 py-1.5 rounded-lg bg-emerald-950 text-emerald-400 border border-emerald-800 hover:bg-emerald-900 transition text-[11px]"
                  >
                    <MessageCircle className="w-3.5 h-3.5" /> Chat on WhatsApp
                  </a>
                </div>
              </div>
            </div>
          </div>

          <div className="mt-12 pt-6 border-t border-stone-900 flex flex-col sm:flex-row justify-between items-center gap-4 text-[11px] text-stone-500">
            <div>
              © 2026 <strong className="text-stone-400 font-semibold">Azlan Fashion</strong>. All rights reserved.
            </div>
            <div className="text-center sm:text-right font-medium text-stone-400">
              Designed, Developed & Maintained by <span className="text-[#D4AF37] font-semibold">Sajid Web Solutions</span>
            </div>
          </div>
        </div>
      </footer>

      {/* Mobile Sticky Bottom Bar */}
      <div className="md:hidden fixed bottom-0 left-0 right-0 z-40 bg-white/95 backdrop-blur-md border-t border-stone-200 py-2 px-4 flex justify-around items-center text-[10px] font-semibold text-stone-600 shadow-xl">
        <button
          onClick={() => { setCurrentPage('home'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
          className={`flex flex-col items-center gap-1 ${currentPage === 'home' ? 'text-stone-950 font-bold' : ''}`}
        >
          <Compass className="w-4 h-4" />
          <span>Home</span>
        </button>
        <button
          onClick={() => { setCurrentPage('shop'); window.scrollTo({ top: 0, behavior: 'smooth' }); }}
          className={`flex flex-col items-center gap-1 ${currentPage === 'shop' ? 'text-stone-950 font-bold' : ''}`}
        >
          <Package className="w-4 h-4" />
          <span>Shop</span>
        </button>
        <button
          onClick={() => setIsReelsModalOpen(true)}
          className="flex flex-col items-center gap-1 text-purple-700 font-bold"
        >
          <Video className="w-4 h-4 text-purple-600" />
          <span>Reels</span>
        </button>
        <button
          onClick={() => setIsWishlistOpen(true)}
          className="flex flex-col items-center gap-1 relative"
        >
          <Heart className="w-4 h-4" />
          <span>Wishlist</span>
          {wishlist.length > 0 && (
            <span className="absolute -top-1 -right-1 bg-rose-600 text-white rounded-full text-[9px] w-3.5 h-3.5 flex items-center justify-center font-bold">
              {wishlist.length}
            </span>
          )}
        </button>
        <button
          onClick={() => setIsCartOpen(true)}
          className="flex flex-col items-center gap-1 relative"
        >
          <ShoppingBag className="w-4 h-4" />
          <span>Bag</span>
          {cart.length > 0 && (
            <span className="absolute -top-1 -right-1 bg-stone-950 text-[#D4AF37] rounded-full text-[9px] w-3.5 h-3.5 flex items-center justify-center font-bold">
              {cart.reduce((t, i) => t + i.quantity, 0)}
            </span>
          )}
        </button>
      </div>
    </div>
  );
}

function HomePage({
  products,
  categories,
  onSelectCategory,
  onOpenProduct,
  onAddToCart,
  onToggleWishlist,
  wishlist,
  onToggleCompare,
  compareList,
  onNavigateShop,
  onWhatsAppOrder,
  onOpenWheel,
  onOpenReels
}) {
  const featuredBags = products.filter((p) => p.isFeatured && p.isActive).slice(0, 4);
  const newArrivals = products.filter((p) => p.isNewArrival && p.isActive).slice(0, 4);

  return (
    <div>
      {/* Hero Showcase */}
      <section className="relative bg-gradient-to-r from-stone-950 via-stone-900 to-stone-950 text-white overflow-hidden py-16 lg:py-24">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
            <div className="lg:col-span-7 space-y-6">
              <div className="inline-flex items-center gap-2 px-3 py-1.5 rounded-full bg-stone-900/90 border border-[#D4AF37]/40 text-[#D4AF37] text-xs font-semibold uppercase tracking-wider">
                <Sparkles className="w-3.5 h-3.5" /> Handcrafted Autumn / Festive Bags 2026
              </div>

              <h1 className="text-4xl sm:text-5xl lg:text-6xl font-serif font-black tracking-tight leading-tight text-white">
                Discover Your <br />
                <span className="italic font-normal text-[#D4AF37]">Perfect Bag</span> Today.
              </h1>

              <p className="text-sm sm:text-base text-stone-300 max-w-xl leading-relaxed">
                Handcrafted luxury satchels, executive laptop bags, and chic sling purses engineered with
                flawless attention to stitch, durability, and contemporary Indian flair.
              </p>

              <div className="pt-2 flex flex-wrap gap-4 items-center">
                <button
                  onClick={onNavigateShop}
                  className="px-8 py-3.5 bg-[#D4AF37] hover:bg-[#c49f2b] text-stone-950 font-bold text-xs uppercase tracking-widest rounded-xl transition shadow-xl flex items-center gap-2"
                >
                  Shop Now <ArrowRight className="w-4 h-4" />
                </button>
                <button
                  onClick={onOpenReels}
                  className="px-6 py-3.5 bg-purple-950 hover:bg-purple-900 text-purple-200 border border-purple-700 font-semibold text-xs uppercase tracking-wider rounded-xl transition flex items-center gap-2"
                >
                  <Video className="w-4 h-4 text-purple-300" /> Watch Reels Lookbook
                </button>
                <button
                  onClick={onOpenWheel}
                  className="px-5 py-3.5 bg-stone-900 hover:bg-stone-800 text-[#D4AF37] border border-[#D4AF37]/50 font-semibold text-xs uppercase tracking-wider rounded-xl transition flex items-center gap-2"
                >
                  <Sparkles className="w-4 h-4 text-[#D4AF37]" /> Spin Lucky Wheel
                </button>
              </div>

              <div className="pt-6 grid grid-cols-3 gap-4 border-t border-stone-800 text-stone-400 text-xs">
                <div className="flex items-center gap-2">
                  <ShieldCheck className="w-4 h-4 text-[#D4AF37]" />
                  <span>100% Genuine Materials</span>
                </div>
                <div className="flex items-center gap-2">
                  <Truck className="w-4 h-4 text-[#D4AF37]" />
                  <span>Express All-India Delivery</span>
                </div>
                <div className="flex items-center gap-2">
                  <RotateCcw className="w-4 h-4 text-[#D4AF37]" />
                  <span>7-Day Replacement Guarantee</span>
                </div>
              </div>
            </div>

            {/* Hero Visual Card */}
            <div className="lg:col-span-5 relative">
              <div className="relative mx-auto max-w-sm rounded-3xl overflow-hidden shadow-2xl border-4 border-stone-800 group">
                <img
                  src="https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80"
                  alt="Azlan Fashion Bag"
                  className="w-full h-[450px] object-cover transition-transform duration-700 group-hover:scale-105"
                />
                <div className="absolute inset-0 bg-gradient-to-t from-stone-950 via-transparent to-transparent opacity-80" />
                <div className="absolute bottom-6 left-6 right-6 p-4 rounded-2xl bg-stone-950/80 backdrop-blur-md border border-stone-700 text-white">
                  <div className="flex justify-between items-center mb-1">
                    <span className="text-[10px] uppercase font-bold tracking-widest text-[#D4AF37]">
                      Featured Masterpiece
                    </span>
                    <span className="text-xs font-bold bg-emerald-600 px-2 py-0.5 rounded text-white">
                      50% OFF
                    </span>
                  </div>
                  <h4 className="text-sm font-serif font-bold">Royal Heritage Leather Satchel</h4>
                  <div className="flex justify-between items-center mt-2 pt-2 border-t border-stone-800">
                    <div>
                      <span className="text-base font-bold text-white">₹2,499</span>
                      <span className="text-xs text-stone-400 line-through ml-2">₹4,999</span>
                    </div>
                    <button
                      onClick={() => onOpenProduct(products[0])}
                      className="text-xs font-semibold text-[#D4AF37] hover:underline flex items-center gap-1"
                    >
                      Quick View <Eye className="w-3.5 h-3.5" />
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Categories Grid Showcase */}
      <section className="py-16 bg-white border-b border-stone-200">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center max-w-2xl mx-auto mb-10">
            <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">
              Curated Wardrobe
            </span>
            <h2 className="text-3xl font-serif font-black text-stone-950 mt-1">
              Explore By Categories
            </h2>
            <p className="text-xs sm:text-sm text-stone-500 mt-2">
              From compact sling essentials to spacious travel weekender holdalls.
            </p>
          </div>

          <div className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4">
            {categories
              .filter((c) => c !== 'All')
              .map((cat) => {
                const sampleProduct = products.find((p) => p.category === cat) || products[0];
                return (
                  <div
                    key={cat}
                    onClick={() => onSelectCategory(cat)}
                    className="group cursor-pointer rounded-2xl border border-stone-200 bg-stone-50 p-3 hover:bg-stone-900 hover:border-stone-900 transition-all duration-300 flex flex-col items-center text-center shadow-xs hover:shadow-lg"
                  >
                    <div className="w-full aspect-square rounded-xl overflow-hidden mb-3 bg-stone-200">
                      <img
                        src={sampleProduct.images[0]}
                        alt={cat}
                        className="w-full h-full object-cover transition duration-500 group-hover:scale-110"
                      />
                    </div>
                    <h3 className="text-xs font-bold text-stone-900 group-hover:text-white transition">
                      {cat}
                    </h3>
                    <span className="text-[10px] text-stone-500 group-hover:text-[#D4AF37] transition mt-0.5">
                      Explore Range &rarr;
                    </span>
                  </div>
                );
              })}
          </div>
        </div>
      </section>

      {/* Featured Products */}
      <section className="py-16 bg-[#FAF8F5]">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col sm:flex-row justify-between items-start sm:items-end mb-8 gap-4">
            <div>
              <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">
                Handpicked Prestige
              </span>
              <h2 className="text-3xl font-serif font-black text-stone-950 mt-1">
                Featured Highlights
              </h2>
            </div>
            <button
              onClick={onNavigateShop}
              className="text-xs font-bold uppercase tracking-widest text-stone-900 hover:text-[#C5A059] flex items-center gap-1.5"
            >
              View Full Catalog ({products.length} bags) <ArrowRight className="w-4 h-4" />
            </button>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {featuredBags.map((product) => (
              <ProductCard
                key={product.id}
                product={product}
                onOpenProduct={onOpenProduct}
                onAddToCart={onAddToCart}
                onToggleWishlist={onToggleWishlist}
                isWishlisted={wishlist.includes(product.id)}
                onToggleCompare={onToggleCompare}
                isCompared={compareList.includes(product.id)}
                onWhatsAppOrder={onWhatsAppOrder}
              />
            ))}
          </div>
        </div>
      </section>

      {/* New Arrivals */}
      <section className="py-16 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center max-w-2xl mx-auto mb-10">
            <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">Fresh off the bench</span>
            <h2 className="text-3xl font-serif font-black text-stone-950 mt-1">New Arrivals</h2>
            <p className="text-xs text-stone-500 mt-2">
              Newly launched silhouettes meticulously crafted with premium fittings.
            </p>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {newArrivals.map((product) => (
              <ProductCard
                key={product.id}
                product={product}
                onOpenProduct={onOpenProduct}
                onAddToCart={onAddToCart}
                onToggleWishlist={onToggleWishlist}
                isWishlisted={wishlist.includes(product.id)}
                onToggleCompare={onToggleCompare}
                isCompared={compareList.includes(product.id)}
                onWhatsAppOrder={onWhatsAppOrder}
              />
            ))}
          </div>
        </div>
      </section>
    </div>
  );
}

function ProductCard({
  product,
  onOpenProduct,
  onAddToCart,
  onToggleWishlist,
  isWishlisted,
  onToggleCompare,
  isCompared,
  onWhatsAppOrder
}) {
  const isOutOfStock = product.stock <= 0;
  const isLowStock = product.stock > 0 && product.stock <= (product.lowStockThreshold || 4);
  const discountPercent = Math.round(((product.mrp - product.price) / product.mrp) * 100);

  return (
    <div className="group bg-white rounded-2xl border border-stone-200 overflow-hidden shadow-xs hover:shadow-xl transition-all duration-300 flex flex-col justify-between">
      <div className="relative aspect-square overflow-hidden bg-stone-100 cursor-pointer" onClick={() => onOpenProduct(product)}>
        <img
          src={product.images && product.images[0] ? product.images[0] : ''}
          alt={product.name}
          className="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
        />

        {/* Badges */}
        <div className="absolute top-3 left-3 flex flex-col gap-1.5 items-start">
          {product.isNewArrival && (
            <span className="bg-stone-950 text-[#D4AF37] text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase tracking-wider shadow">
              New
            </span>
          )}
          {discountPercent > 0 && (
            <span className="bg-rose-600 text-white text-[10px] font-bold px-2 py-0.5 rounded-md shadow">
              {discountPercent}% OFF
            </span>
          )}
        </div>

        {/* Action icons */}
        <div className="absolute top-3 right-3 flex flex-col gap-2">
          <button
            onClick={(e) => {
              e.stopPropagation();
              onToggleWishlist(product.id);
            }}
            className="w-8 h-8 rounded-full bg-white/90 text-stone-800 flex items-center justify-center transition shadow hover:bg-stone-950 hover:text-white"
            title="Save to Wishlist"
          >
            <Heart className={`w-4 h-4 ${isWishlisted ? 'text-rose-600 fill-current' : ''}`} />
          </button>
          <button
            onClick={(e) => {
              e.stopPropagation();
              onToggleCompare(product.id);
            }}
            className={`w-8 h-8 rounded-full flex items-center justify-center transition shadow ${
              isCompared ? 'bg-stone-900 text-[#D4AF37]' : 'bg-white/90 text-stone-800 hover:bg-stone-950 hover:text-white'
            }`}
            title="Compare Bag Specs"
          >
            <Scale className="w-4 h-4" />
          </button>
        </div>

        {/* Stock Badge */}
        <div className="absolute bottom-3 left-3">
          {isOutOfStock ? (
            <span className="bg-rose-700 text-white text-[10px] font-bold px-2.5 py-1 rounded-md">
              Out of Stock
            </span>
          ) : isLowStock ? (
            <span className="bg-amber-600 text-white text-[10px] font-bold px-2 py-0.5 rounded-md shadow">
              Only {product.stock} left!
            </span>
          ) : (
            <span className="bg-stone-900/80 text-stone-200 text-[10px] font-medium px-2 py-0.5 rounded-md backdrop-blur-xs">
              {product.stock} in stock
            </span>
          )}
        </div>
      </div>

      <div className="p-4 flex-1 flex flex-col justify-between">
        <div>
          <div className="flex items-center justify-between text-[11px] text-stone-500 mb-1">
            <span className="font-semibold uppercase tracking-wider text-[#C5A059]">{product.category}</span>
            <div className="flex items-center gap-1 text-amber-500">
              <Star className="w-3 h-3 fill-current" />
              <span className="font-bold text-stone-800">{product.rating}</span>
            </div>
          </div>

          <h3
            onClick={() => onOpenProduct(product)}
            className="text-xs sm:text-sm font-serif font-bold text-stone-950 line-clamp-1 cursor-pointer hover:text-[#C5A059] transition"
          >
            {product.name}
          </h3>

          <div className="flex items-baseline gap-2 mt-2">
            <span className="text-base font-black text-stone-950">₹{product.price.toLocaleString('en-IN')}</span>
            <span className="text-xs text-stone-400 line-through">₹{product.mrp.toLocaleString('en-IN')}</span>
          </div>
        </div>

        <div className="pt-3 border-t border-stone-100 mt-3 grid grid-cols-2 gap-2">
          <button
            disabled={isOutOfStock}
            onClick={() => onAddToCart(product, 1, '', '', true)}
            className={`py-2 px-2 rounded-lg text-[11px] font-bold uppercase tracking-wider transition flex items-center justify-center gap-1 ${
              isOutOfStock
                ? 'bg-stone-100 text-stone-400 cursor-not-allowed border border-stone-200'
                : 'bg-stone-900 hover:bg-stone-800 text-[#D4AF37]'
            }`}
          >
            <ShoppingBag className="w-3.5 h-3.5" />
            {isOutOfStock ? 'Sold Out' : 'Add to Bag'}
          </button>
          <button
            disabled={isOutOfStock}
            onClick={() => onWhatsAppOrder(product)}
            className={`py-2 px-2 rounded-lg text-[11px] font-semibold transition flex items-center justify-center gap-1 ${
              isOutOfStock
                ? 'bg-stone-100 text-stone-400 cursor-not-allowed border border-stone-200'
                : 'bg-emerald-700 hover:bg-emerald-800 text-white'
            }`}
          >
            <MessageCircle className="w-3.5 h-3.5" /> Buy Now
          </button>
        </div>
      </div>
    </div>
  );
}

function ShopPage({
  products,
  categories,
  selectedCategory,
  setSelectedCategory,
  searchQuery,
  setSearchQuery,
  sortBy,
  setSortBy,
  priceFilter,
  setPriceFilter,
  onlyInStock,
  setOnlyInStock,
  onOpenProduct,
  onAddToCart,
  onToggleWishlist,
  wishlist,
  onToggleCompare,
  compareList,
  onWhatsAppOrder
}) {
  const [mobileFilterOpen, setMobileFilterOpen] = useState(false);

  return (
    <div className="py-8 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div className="mb-6">
        <span className="text-xs font-medium text-stone-500">
          Home / Shop / <strong className="text-stone-900">{selectedCategory}</strong>
        </span>
        <h1 className="text-3xl font-serif font-black text-stone-950 mt-1">Azlan Bag Collections</h1>
        <p className="text-xs text-stone-500 mt-1">
          Showing {products.length} handcrafted bag designs with real-time stock availability
        </p>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-4 gap-8">
        <aside className="hidden lg:block space-y-6 bg-white p-6 rounded-2xl border border-stone-200 h-fit">
          <div className="flex items-center justify-between pb-3 border-b border-stone-200">
            <h3 className="text-sm font-serif font-bold text-stone-900 flex items-center gap-2">
              <SlidersHorizontal className="w-4 h-4 text-[#D4AF37]" /> Filter Collection
            </h3>
            {(selectedCategory !== 'All' || searchQuery || onlyInStock || priceFilter < 10000) && (
              <button
                onClick={() => {
                  setSelectedCategory('All');
                  setSearchQuery('');
                  setOnlyInStock(false);
                  setPriceFilter(10000);
                }}
                className="text-[11px] text-[#C5A059] hover:underline font-semibold"
              >
                Reset All
              </button>
            )}
          </div>

          <div>
            <label className="text-xs font-bold uppercase tracking-wider text-stone-700 block mb-2.5">
              Categories
            </label>
            <div className="space-y-1 max-h-56 overflow-y-auto pr-1">
              {categories.map((cat) => (
                <button
                  key={cat}
                  onClick={() => setSelectedCategory(cat)}
                  className={`w-full text-left px-2.5 py-1.5 rounded-lg text-xs font-medium transition flex items-center justify-between ${
                    selectedCategory === cat ? 'bg-stone-900 text-white' : 'text-stone-600 hover:bg-stone-100'
                  }`}
                >
                  <span>{cat}</span>
                  {selectedCategory === cat && <Check className="w-3.5 h-3.5 text-[#D4AF37]" />}
                </button>
              ))}
            </div>
          </div>

          <div className="pt-4 border-t border-stone-100">
            <div className="flex justify-between items-center mb-2">
              <label className="text-xs font-bold uppercase tracking-wider text-stone-700">Max Price</label>
              <span className="text-xs font-bold text-stone-900">₹{priceFilter.toLocaleString('en-IN')}</span>
            </div>
            <input
              type="range"
              min="500"
              max="10000"
              step="250"
              value={priceFilter}
              onChange={(e) => setPriceFilter(Number(e.target.value))}
              className="w-full accent-[#D4AF37] cursor-pointer"
            />
            <div className="flex justify-between text-[10px] text-stone-400 mt-1">
              <span>₹500</span>
              <span>₹10,000+</span>
            </div>
          </div>

          <div className="pt-4 border-t border-stone-100">
            <label className="flex items-center gap-2 cursor-pointer text-xs font-medium text-stone-700">
              <input
                type="checkbox"
                checked={onlyInStock}
                onChange={(e) => setOnlyInStock(e.target.checked)}
                className="rounded accent-stone-950 w-4 h-4 cursor-pointer"
              />
              <span>In-Stock Items Only</span>
            </label>
          </div>
        </aside>

        {/* Product Catalog Display */}
        <div className="lg:col-span-3 space-y-6">
          <div className="bg-white p-4 rounded-xl border border-stone-200 flex flex-wrap items-center justify-between gap-4">
            <div className="flex items-center gap-2">
              <button
                onClick={() => setMobileFilterOpen(!mobileFilterOpen)}
                className="lg:hidden px-3 py-1.5 rounded-lg border border-stone-300 text-xs font-semibold flex items-center gap-1.5"
              >
                <Filter className="w-3.5 h-3.5" /> Filters
              </button>
              <span className="text-xs font-medium text-stone-600">
                Showing <strong className="text-stone-950">{products.length}</strong> items
              </span>
            </div>

            <div className="flex items-center gap-2 text-xs">
              <span className="text-stone-500 font-medium">Sort By:</span>
              <select
                value={sortBy}
                onChange={(e) => setSortBy(e.target.value)}
                className="px-2.5 py-1.5 rounded-lg border border-stone-300 bg-stone-50 text-stone-800 font-medium focus:outline-none"
              >
                <option value="featured">Featured Picks</option>
                <option value="newest">New Arrivals</option>
                <option value="price-low">Price: Low to High</option>
                <option value="price-high">Price: High to Low</option>
                <option value="rating">Customer Rating</option>
              </select>
            </div>
          </div>

          {products.length === 0 ? (
            <div className="bg-white rounded-2xl border border-stone-200 p-12 text-center">
              <Search className="w-10 h-10 mx-auto text-stone-400 mb-3" />
              <h3 className="text-base font-serif font-bold text-stone-900">No bags match your criteria</h3>
              <p className="text-xs text-stone-500 mt-1 max-w-sm mx-auto">
                Try widening your price range or clearing selected category filters.
              </p>
              <button
                onClick={() => {
                  setSelectedCategory('All');
                  setSearchQuery('');
                  setOnlyInStock(false);
                  setPriceFilter(10000);
                }}
                className="mt-4 px-5 py-2 bg-stone-900 text-[#D4AF37] text-xs font-semibold rounded-lg"
              >
                Clear Filters
              </button>
            </div>
          ) : (
            <div className="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-6">
              {products.map((product) => (
                <ProductCard
                  key={product.id}
                  product={product}
                  onOpenProduct={onOpenProduct}
                  onAddToCart={onAddToCart}
                  onToggleWishlist={onToggleWishlist}
                  isWishlisted={wishlist.includes(product.id)}
                  onToggleCompare={onToggleCompare}
                  isCompared={compareList.includes(product.id)}
                  onWhatsAppOrder={onWhatsAppOrder}
                />
              ))}
            </div>
          )}
        </div>
      </div>
    </div>
  );
}

function CategoriesExplorerPage({ categories, products, onSelectCategory }) {
  return (
    <div className="py-12 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div className="text-center max-w-2xl mx-auto mb-12">
        <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">Categorical Lookbook</span>
        <h1 className="text-3xl sm:text-4xl font-serif font-black text-stone-950 mt-1">Explore By Silhouettes</h1>
        <p className="text-xs sm:text-sm text-stone-500 mt-2">
          From work backpacks to bespoke party clutches, each category is curated for lasting functionality.
        </p>
      </div>

      <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
        {categories
          .filter((c) => c !== 'All')
          .map((cat) => {
            const catProducts = products.filter((p) => p.category === cat);
            const coverProduct = catProducts[0] || products[0];

            return (
              <div
                key={cat}
                onClick={() => onSelectCategory(cat)}
                className="group relative rounded-3xl overflow-hidden bg-white border border-stone-200 shadow-sm hover:shadow-2xl transition duration-500 cursor-pointer flex flex-col justify-between"
              >
                <div className="aspect-[4/3] overflow-hidden bg-stone-100">
                  <img
                    src={coverProduct.images[0]}
                    alt={cat}
                    className="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105"
                  />
                </div>
                <div className="p-6">
                  <div className="flex justify-between items-center">
                    <h3 className="text-lg font-serif font-bold text-stone-950 group-hover:text-[#C5A059] transition">
                      {cat}
                    </h3>
                    <span className="text-xs px-2 py-0.5 rounded-full bg-stone-100 font-semibold text-stone-600">
                      {catProducts.length} Models
                    </span>
                  </div>
                  <p className="text-xs text-stone-500 mt-2 line-clamp-2">
                    Hand-inspected {cat.toLowerCase()} collection with reinforced zippers, durable lining and stylish silhouettes.
                  </p>
                  <div className="mt-4 pt-3 border-t border-stone-100 flex items-center justify-between text-xs font-bold text-stone-900 group-hover:text-[#D4AF37] transition">
                    <span>Shop All in {cat}</span>
                    <ArrowRight className="w-4 h-4 transform group-hover:translate-x-1 transition" />
                  </div>
                </div>
              </div>
            );
          })}
      </div>
    </div>
  );
}

function AboutUsPage() {
  return (
    <div className="py-14 max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 space-y-12">
      <div className="text-center space-y-3">
        <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">The Azlan Story</span>
        <h1 className="text-3xl sm:text-5xl font-serif font-black text-stone-950">
          Where Heritage Craft Meets Modern Purpose
        </h1>
        <p className="text-sm text-stone-600 max-w-2xl mx-auto leading-relaxed">
          Founded with an ambition to revolutionize everyday leather goods, Azlan Fashion blends timeless Indian artisanship with forward-thinking minimalist design.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-8 items-center bg-white p-8 rounded-3xl border border-stone-200 shadow-sm">
        <div className="aspect-square rounded-2xl overflow-hidden shadow-md">
          <img
            src="https://images.unsplash.com/photo-1548036328-c9fa89d128fa?auto=format&fit=crop&w=800&q=80"
            alt="Handcrafting Bag"
            className="w-full h-full object-cover"
          />
        </div>
        <div className="space-y-4">
          <h3 className="text-2xl font-serif font-bold text-stone-950">No Shortcuts in Craftsmanship</h3>
          <p className="text-xs leading-relaxed text-stone-600">
            Every stitch in an Azlan handbag or backpack is designed to endure. We rigorously source verified high-grade leathers, weather-resistant ballistic textiles, and robust multi-plated zinc alloy fittings.
          </p>
          <div className="space-y-2 pt-2">
            <div className="flex items-center gap-2 text-xs font-semibold text-stone-800">
              <CheckCircle className="w-4 h-4 text-emerald-600" /> Hand-Finished Edge Coating & Heavy Stitching
            </div>
            <div className="flex items-center gap-2 text-xs font-semibold text-stone-800">
              <CheckCircle className="w-4 h-4 text-emerald-600" /> Ergonomic Weight Distribution on Straps
            </div>
            <div className="flex items-center gap-2 text-xs font-semibold text-stone-800">
              <CheckCircle className="w-4 h-4 text-emerald-600" /> Direct Manufacturer Pricing with Zero Middlemen
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

function ContactPage({ onWhatsAppOrder }) {
  return (
    <div className="py-12 max-w-5xl mx-auto px-4 sm:px-6 lg:px-8 space-y-10">
      <div className="text-center space-y-2">
        <span className="text-xs font-bold uppercase tracking-widest text-[#C5A059]">Direct Store Concierge</span>
        <h1 className="text-3xl sm:text-4xl font-serif font-black text-stone-950">We are Here to Help</h1>
        <p className="text-xs sm:text-sm text-stone-500 max-w-lg mx-auto">
          Have questions regarding bag sizes, corporate customization or delivery tracking? Reach out directly.
        </p>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div className="bg-white p-6 rounded-2xl border border-stone-200 shadow-xs flex flex-col items-center text-center space-y-3">
          <div className="w-12 h-12 rounded-full bg-amber-50 text-[#C5A059] flex items-center justify-center">
            <Phone className="w-6 h-6" />
          </div>
          <h4 className="text-sm font-serif font-bold text-stone-900">Phone Support</h4>
          <p className="text-xs text-stone-500">Available Mon-Sat 10am to 8pm IST</p>
          <a
            href="tel:7762067143"
            className="text-xs font-bold text-stone-950 hover:text-[#C5A059] px-4 py-2 rounded-lg bg-stone-100 hover:bg-stone-200 transition"
          >
            +91 7762067143
          </a>
        </div>

        <div className="bg-white p-6 rounded-2xl border border-stone-200 shadow-xs flex flex-col items-center text-center space-y-3">
          <div className="w-12 h-12 rounded-full bg-emerald-50 text-emerald-600 flex items-center justify-center">
            <MessageCircle className="w-6 h-6" />
          </div>
          <h4 className="text-sm font-serif font-bold text-stone-900">Instant WhatsApp</h4>
          <p className="text-xs text-stone-500">Quick product photos and instant ordering</p>
          <a
            href="https://wa.me/917762067143"
            target="_blank"
            rel="noreferrer"
            className="text-xs font-bold text-white px-4 py-2 rounded-lg bg-emerald-700 hover:bg-emerald-800 transition"
          >
            Open WhatsApp Chat
          </a>
        </div>

        <div className="bg-white p-6 rounded-2xl border border-stone-200 shadow-xs flex flex-col items-center text-center space-y-3">
          <div className="w-12 h-12 rounded-full bg-stone-100 text-stone-800 flex items-center justify-center">
            <Mail className="w-6 h-6" />
          </div>
          <h4 className="text-sm font-serif font-bold text-stone-900">Email Inquiry</h4>
          <p className="text-xs text-stone-500">Bulk orders and corporate collaborations</p>
          <a
            href="mailto:workwithsajid@zohomail.in"
            className="text-xs font-bold text-stone-950 hover:text-[#C5A059] px-3 py-2 rounded-lg bg-stone-100 hover:bg-stone-200 transition truncate max-w-full"
          >
            workwithsajid@zohomail.in
          </a>
        </div>
      </div>
    </div>
  );
}

function PoliciesPage() {
  return (
    <div className="py-12 max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 space-y-8">
      <div className="border-b border-stone-200 pb-4">
        <h1 className="text-3xl font-serif font-black text-stone-950">Customer Terms & Policies</h1>
        <p className="text-xs text-stone-500 mt-1">Azlan Fashion Store Guidelines & Guarantees</p>
      </div>

      <div className="space-y-6 text-xs text-stone-700 leading-relaxed bg-white p-6 sm:p-8 rounded-2xl border border-stone-200">
        <div>
          <h3 className="text-sm font-serif font-bold text-stone-950 mb-1">1. All-India Shipping Policy</h3>
          <p>
            Orders are processed and dispatched within 24-48 business hours from our central warehouse. Standard delivery timelines range from 3 to 5 working days across metro and non-metro pin codes. Express tracking details are automatically shared via SMS and WhatsApp once shipped.
          </p>
        </div>

        <div>
          <h3 className="text-sm font-serif font-bold text-stone-950 mb-1">2. 7-Day Replacement Guarantee</h3>
          <p>
            We inspect each handbag, sling, and backpack meticulously before packaging. If your item arrives damaged, flawed, or differs from the catalog images, you can initiate a hassle-free exchange within 7 days by contacting us on WhatsApp at <strong>+91 7762067143</strong>.
          </p>
        </div>

        <div>
          <h3 className="text-sm font-serif font-bold text-stone-950 mb-1">3. Privacy & Data Security</h3>
          <p>
            Customer details including phone numbers, physical addresses, and order histories are handled strictly for shipment routing and fulfillment. We never sell or share customer credentials.
          </p>
        </div>
      </div>
    </div>
  );
}

function AdminLoginPage({ email, setEmail, password, setPassword, onSubmit, error, isLoading, onBackToStore }) {
  return (
    <div className="min-h-[75vh] flex items-center justify-center p-4">
      <div className="max-w-md w-full bg-white rounded-3xl border border-stone-200 shadow-2xl p-8 space-y-6">
        <div className="text-center space-y-2">
          <div className="w-12 h-12 rounded-2xl bg-stone-950 text-[#D4AF37] flex items-center justify-center mx-auto shadow-md">
            <Lock className="w-6 h-6" />
          </div>
          <h2 className="text-2xl font-serif font-black text-stone-950">Staff & Admin Portal</h2>
          <p className="text-xs text-stone-500">
            Secure ERP authentication for Azlan Fashion inventory & order operations.
          </p>
        </div>

        {error && (
          <div className="p-3 rounded-xl bg-rose-50 border border-rose-200 text-rose-700 text-xs flex items-center gap-2">
            <AlertTriangle className="w-4 h-4 shrink-0" />
            <span>{error}</span>
          </div>
        )}

        <form onSubmit={onSubmit} className="space-y-4">
          <div>
            <label className="text-xs font-bold text-stone-700 block mb-1">Admin Email</label>
            <div className="relative">
              <input
                type="email"
                required
                value={email}
                onChange={(e) => setEmail(e.target.value)}
                placeholder="workwithsajid@zohomail.in"
                className="w-full pl-9 pr-3 py-2.5 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
              />
              <User className="w-4 h-4 text-stone-400 absolute left-3 top-3" />
            </div>
          </div>

          <div>
            <label className="text-xs font-bold text-stone-700 block mb-1">Admin Password</label>
            <div className="relative">
              <input
                type="password"
                required
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                placeholder="••••••••••••"
                className="w-full pl-9 pr-3 py-2.5 text-xs rounded-xl border border-stone-300 focus:outline-none focus:ring-1 focus:ring-[#D4AF37]"
              />
              <Key className="w-4 h-4 text-stone-400 absolute left-3 top-3" />
            </div>
          </div>

          <button
            type="submit"
            disabled={isLoading}
            className="w-full py-3 bg-stone-950 hover:bg-stone-900 text-[#D4AF37] font-bold text-xs uppercase tracking-widest rounded-xl transition shadow-lg"
          >
            {isLoading ? 'Verifying...' : 'Enter Admin Suite'}
          </button>
        </form>

        <div className="pt-2 text-center">
          <button onClick={onBackToStore} className="text-xs text-stone-500 hover:text-stone-900 font-medium">
            &larr; Return to Customer Store
          </button>
        </div>
      </div>
    </div>
  );
}

function AdminDashboardPage({
  adminUser,
  onLogout,
  adminTab,
  setAdminTab,
  products,
  orders,
  categories,
  coupons,
  abandonedCarts,
  onRecoverAbandonedCart,
  onQuickStock,
  onExactStock,
  onOrderStatusChange,
  onDeleteProduct,
  onOpenAddProduct,
  onOpenEditProduct,
  onAddCategory,
  onDeleteCategory,
  onExportCSV,
  onViewInvoice,
  onViewShippingLabel,
  showToast
}) {
  const totalProducts = products.length;
  const totalStockUnits = products.reduce((sum, p) => sum + p.stock, 0);
  const outOfStockCount = products.filter((p) => p.stock <= 0).length;
  const lowStockCount = products.filter((p) => p.stock > 0 && p.stock <= (p.lowStockThreshold || 4)).length;
  const totalSalesRevenue = orders
    .filter((o) => o.status !== 'Cancelled')
    .reduce((sum, o) => sum + o.totalAmount, 0);

  const [newCatInput, setNewCatInput] = useState('');

  return (
    <div className="bg-[#FAF8F5] min-h-screen py-8">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-8">
        {/* Header */}
        <div className="bg-stone-950 text-white rounded-3xl p-6 shadow-xl flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
          <div className="flex items-center gap-3">
            <div className="w-12 h-12 rounded-2xl bg-[#D4AF37] text-stone-950 flex items-center justify-center font-bold text-xl">
              <LayoutDashboard className="w-6 h-6" />
            </div>
            <div>
              <div className="flex items-center gap-2">
                <h1 className="text-xl font-serif font-bold text-white">Azlan Fashion Admin ERP</h1>
                <span className="text-[10px] bg-[#D4AF37]/20 text-[#D4AF37] border border-[#D4AF37]/40 px-2 py-0.5 rounded-full font-semibold">
                  Live Terminal
                </span>
              </div>
              <p className="text-xs text-stone-400">
                Logged in as: <strong className="text-stone-200">{adminUser?.email || 'workwithsajid@zohomail.in'}</strong>
              </p>
            </div>
          </div>

          <div className="flex items-center gap-2.5">
            <button
              onClick={onExportCSV}
              className="px-3.5 py-2 bg-stone-900 hover:bg-stone-800 text-stone-200 border border-stone-800 rounded-xl text-xs font-semibold flex items-center gap-1.5 transition"
            >
              <Download className="w-3.5 h-3.5 text-[#D4AF37]" /> Export Orders CSV
            </button>
            <button
              onClick={onLogout}
              className="px-4 py-2 bg-rose-950 hover:bg-rose-900 text-rose-300 rounded-xl text-xs font-semibold flex items-center gap-1.5 transition"
            >
              <LogOut className="w-3.5 h-3.5" /> Logout
            </button>
          </div>
        </div>

        {/* Tab Selector */}
        <div className="flex gap-2 overflow-x-auto pb-1 border-b border-stone-200">
          {[
            { id: 'overview', label: 'Dashboard Overview', icon: TrendingUp },
            { id: 'abandoned', label: `Abandoned Carts (${abandonedCarts.filter(a => !a.recovered).length})`, icon: RefreshCw },
            { id: 'products', label: `Products (${totalProducts})`, icon: Package },
            { id: 'inventory', label: `Live Inventory (${totalStockUnits})`, icon: Boxes },
            { id: 'orders', label: `Orders (${orders.length})`, icon: ClipboardList },
            { id: 'categories', label: `Categories (${categories.length})`, icon: Layers },
            { id: 'coupons', label: `Coupons (${coupons.length})`, icon: Tag }
          ].map((tab) => {
            const Icon = tab.icon;
            return (
              <button
                key={tab.id}
                onClick={() => setAdminTab(tab.id)}
                className={`px-4 py-2.5 rounded-xl text-xs font-bold transition flex items-center gap-2 shrink-0 ${
                  adminTab === tab.id
                    ? 'bg-stone-900 text-[#D4AF37] shadow-md'
                    : 'bg-white text-stone-600 hover:bg-stone-100 border border-stone-200'
                }`}
              >
                <Icon className="w-4 h-4" />
                <span>{tab.label}</span>
              </button>
            );
          })}
        </div>

        {/* Tab 1: Overview */}
        {adminTab === 'overview' && (
          <div className="space-y-6">
            <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div className="bg-white p-5 rounded-2xl border border-stone-200">
                <span className="text-[11px] font-bold uppercase text-stone-500">Total Sales</span>
                <div className="text-2xl font-black text-stone-950 mt-1">₹{totalSalesRevenue.toLocaleString('en-IN')}</div>
                <span className="text-[11px] text-emerald-700 font-semibold">{orders.length} Total Orders</span>
              </div>
              <div className="bg-white p-5 rounded-2xl border border-stone-200">
                <span className="text-[11px] font-bold uppercase text-stone-500">Active Stock</span>
                <div className="text-2xl font-black text-stone-950 mt-1">{totalStockUnits} Units</div>
                <span className="text-[11px] text-stone-500">{totalProducts} Catalog items</span>
              </div>
              <div className="bg-white p-5 rounded-2xl border border-stone-200">
                <span className="text-[11px] font-bold uppercase text-stone-500">Low Stock Alert</span>
                <div className="text-2xl font-black text-amber-600 mt-1">{lowStockCount} Bags</div>
                <span className="text-[11px] text-amber-700">Stock ≤ 4 items</span>
              </div>
              <div className="bg-white p-5 rounded-2xl border border-stone-200">
                <span className="text-[11px] font-bold uppercase text-stone-500">Sold Out (Stock 0)</span>
                <div className="text-2xl font-black text-rose-600 mt-1">{outOfStockCount} Bags</div>
                <span className="text-[11px] text-rose-700">Replenish ASAP</span>
              </div>
            </div>

            {/* Quick Orders Overview */}
            <div className="bg-white rounded-2xl border border-stone-200 p-6">
              <h3 className="text-base font-serif font-bold text-stone-950 mb-3">Recent Orders</h3>
              <div className="overflow-x-auto">
                <table className="w-full text-left text-xs">
                  <thead className="bg-stone-50 text-stone-500 uppercase font-bold border-b border-stone-200">
                    <tr>
                      <th className="p-3">Order ID</th>
                      <th className="p-3">Customer</th>
                      <th className="p-3">Total Amount</th>
                      <th className="p-3">Status</th>
                      <th className="p-3 text-right">Actions</th>
                    </tr>
                  </thead>
                  <tbody className="divide-y divide-stone-100">
                    {orders.slice(0, 5).map((ord) => (
                      <tr key={ord.id}>
                        <td className="p-3 font-bold text-stone-900">{ord.id}</td>
                        <td className="p-3">
                          <span className="font-semibold">{ord.customerName}</span>
                          <span className="text-[10px] text-stone-400 block">{ord.phone}</span>
                        </td>
                        <td className="p-3 font-bold">₹{ord.totalAmount.toLocaleString('en-IN')}</td>
                        <td className="p-3">
                          <span className="px-2 py-0.5 rounded-full text-[10px] font-bold uppercase bg-stone-100 text-stone-800">
                            {ord.status}
                          </span>
                        </td>
                        <td className="p-3 text-right space-x-2">
                          <button
                            onClick={() => onViewShippingLabel(ord)}
                            className="p-1.5 rounded-lg bg-stone-100 hover:bg-stone-200 text-stone-700"
                            title="Print Parcel Label"
                          >
                            <Barcode className="w-3.5 h-3.5" />
                          </button>
                          <button
                            onClick={() => onViewInvoice(ord)}
                            className="p-1.5 rounded-lg bg-stone-100 hover:bg-stone-200 text-stone-700"
                            title="Print GST Invoice"
                          >
                            <Printer className="w-3.5 h-3.5" />
                          </button>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        )}

        {/* Tab: Abandoned Cart WhatsApp Recovery */}
        {adminTab === 'abandoned' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <div className="flex justify-between items-center">
              <div>
                <h3 className="text-lg font-serif font-bold text-stone-950">Abandoned Cart WhatsApp Recovery Desk</h3>
                <p className="text-xs text-stone-500">
                  Send personalized WhatsApp recovery messages with an exclusive 10% coupon with a single tap.
                </p>
              </div>
            </div>

            <div className="space-y-3">
              {abandonedCarts.map((item) => (
                <div key={item.id} className="p-4 rounded-xl border border-stone-200 bg-stone-50/50 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
                  <div>
                    <div className="flex items-center gap-2">
                      <span className="font-bold text-stone-900 text-xs">{item.customerName}</span>
                      <span className="text-[10px] text-stone-400">Phone: {item.phone}</span>
                      <span className="text-[10px] bg-amber-100 text-amber-800 px-2 py-0.5 rounded-full font-semibold">
                        Left {item.abandonedAt}
                      </span>
                    </div>
                    <p className="text-xs text-stone-600 mt-1">
                      <strong>Cart Items:</strong> {item.itemNames} • <strong>Value:</strong> ₹{item.cartValue.toLocaleString('en-IN')}
                    </p>
                  </div>

                  <button
                    onClick={() => onRecoverAbandonedCart(item)}
                    className={`px-4 py-2 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition ${
                      item.recovered
                        ? 'bg-stone-200 text-stone-600 cursor-default'
                        : 'bg-emerald-700 hover:bg-emerald-800 text-white'
                    }`}
                  >
                    <Send className="w-3.5 h-3.5" />
                    {item.recovered ? 'Recovery Sent' : 'Send WhatsApp Recovery'}
                  </button>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* Tab 2: Products */}
        {adminTab === 'products' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <div className="flex justify-between items-center">
              <div>
                <h3 className="text-lg font-serif font-bold text-stone-950">Catalog Products</h3>
                <p className="text-xs text-stone-500">Edit prices, stocks, and descriptions.</p>
              </div>
              <button
                onClick={onOpenAddProduct}
                className="px-4 py-2 bg-stone-950 text-[#D4AF37] font-bold text-xs uppercase rounded-xl flex items-center gap-1.5"
              >
                <Plus className="w-4 h-4" /> Add Product
              </button>
            </div>

            <div className="overflow-x-auto">
              <table className="w-full text-left text-xs">
                <thead className="bg-stone-50 text-stone-500 uppercase font-bold border-b border-stone-200">
                  <tr>
                    <th className="p-3">Bag Title</th>
                    <th className="p-3">Category</th>
                    <th className="p-3">Price</th>
                    <th className="p-3">Stock</th>
                    <th className="p-3 text-right">Actions</th>
                  </tr>
                </thead>
                <tbody className="divide-y divide-stone-100">
                  {products.map((p) => (
                    <tr key={p.id}>
                      <td className="p-3 flex items-center gap-3">
                        <img src={p.images && p.images[0] ? p.images[0] : ''} alt="" className="w-10 h-12 object-cover rounded-lg bg-stone-100" />
                        <span className="font-bold text-stone-900">{p.name}</span>
                      </td>
                      <td className="p-3">{p.category}</td>
                      <td className="p-3 font-bold">₹{p.price.toLocaleString('en-IN')}</td>
                      <td className="p-3 font-bold">{p.stock} units</td>
                      <td className="p-3 text-right space-x-2">
                        <button onClick={() => onOpenEditProduct(p)} className="p-1.5 rounded-lg bg-stone-100 text-stone-700">
                          <Edit className="w-3.5 h-3.5" />
                        </button>
                        <button onClick={() => onDeleteProduct(p.id)} className="p-1.5 rounded-lg bg-rose-50 text-rose-600">
                          <Trash2 className="w-3.5 h-3.5" />
                        </button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        )}

        {/* Tab 3: Live Inventory */}
        {adminTab === 'inventory' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <h3 className="text-lg font-serif font-bold text-stone-950">Real-Time Inventory Terminal</h3>
            <div className="grid grid-cols-1 gap-3">
              {products.map((p) => (
                <div key={p.id} className="p-3 rounded-xl border border-stone-200 flex items-center justify-between">
                  <div className="flex items-center gap-3">
                    <img src={p.images && p.images[0] ? p.images[0] : ''} alt="" className="w-12 h-14 object-cover rounded-lg bg-stone-100" />
                    <div>
                      <h4 className="text-xs font-bold text-stone-900">{p.name}</h4>
                      <p className="text-[11px] text-stone-500">Category: {p.category}</p>
                    </div>
                  </div>
                  <div className="flex items-center gap-3">
                    <div className="flex items-center border border-stone-300 rounded-xl overflow-hidden">
                      <button onClick={() => onQuickStock(p.id, -1)} className="px-3 py-1 text-xs font-bold hover:bg-stone-100">-</button>
                      <input
                        type="number"
                        min="0"
                        value={p.stock}
                        onChange={(e) => onExactStock(p.id, e.target.value)}
                        className="w-16 text-center text-xs font-bold border-x border-stone-200 py-1"
                      />
                      <button onClick={() => onQuickStock(p.id, 1)} className="px-3 py-1 text-xs font-bold hover:bg-stone-100">+</button>
                    </div>
                    <button onClick={() => onQuickStock(p.id, 10)} className="px-3 py-1.5 bg-stone-100 hover:bg-stone-200 text-stone-800 text-xs font-semibold rounded-xl">
                      +10 Restock
                    </button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* Tab 4: Orders & Shipping Labels */}
        {adminTab === 'orders' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <div className="flex justify-between items-center">
              <div>
                <h3 className="text-lg font-serif font-bold text-stone-950">Customer Orders Fulfillment</h3>
                <p className="text-xs text-stone-500">Manage Delhivery AWBs, print parcel labels, and update milestones.</p>
              </div>
              <button
                onClick={onExportCSV}
                className="px-3 py-1.5 bg-stone-900 text-white text-xs font-semibold rounded-xl flex items-center gap-1.5"
              >
                <Download className="w-3.5 h-3.5 text-[#D4AF37]" /> Export CSV
              </button>
            </div>

            <div className="space-y-3">
              {orders.map((ord) => (
                <div key={ord.id} className="p-4 rounded-xl border border-stone-200 bg-stone-50/50 space-y-2">
                  <div className="flex justify-between items-center flex-wrap gap-2">
                    <div className="flex items-center gap-2">
                      <span className="font-bold text-stone-900">{ord.id}</span>
                      <span className="text-xs bg-stone-200 text-stone-800 px-2 py-0.5 rounded-full font-semibold">{ord.status}</span>
                      <span className="text-[10px] text-stone-400">{ord.date}</span>
                    </div>
                    <div className="flex items-center gap-2">
                      <button
                        onClick={() => onViewShippingLabel(ord)}
                        className="px-2.5 py-1 bg-stone-900 text-[#D4AF37] rounded-lg text-xs font-bold flex items-center gap-1 shadow-sm"
                      >
                        <Barcode className="w-3 h-3" /> Parcel Sticker
                      </button>
                      <button
                        onClick={() => onViewInvoice(ord)}
                        className="px-2.5 py-1 bg-stone-100 hover:bg-stone-200 rounded-lg text-xs font-semibold flex items-center gap-1 text-stone-700"
                      >
                        <Printer className="w-3 h-3" /> GST Bill
                      </button>
                      <select
                        value={ord.status}
                        onChange={(e) => onOrderStatusChange(ord.id, e.target.value)}
                        className="text-xs font-bold border rounded-lg p-1 bg-white"
                      >
                        <option value="Pending">Pending</option>
                        <option value="Confirmed">Confirmed</option>
                        <option value="Packed">Packed</option>
                        <option value="Shipped">Shipped</option>
                        <option value="Delivered">Delivered</option>
                        <option value="Cancelled">Cancelled (Restores Stock)</option>
                      </select>
                    </div>
                  </div>
                  <div className="text-xs text-stone-600">
                    <p><strong>Customer:</strong> {ord.customerName} ({ord.phone}) • {ord.address}, {ord.city} - {ord.pincode}</p>
                    <p><strong>Items:</strong> {ord.items.map((i) => `${i.name} (x${i.qty})`).join(', ')}</p>
                    {ord.monogramDetails && (
                      <p className="text-stone-900 font-semibold">
                        🔤 Monogram Request: "{ord.monogramDetails.text}" ({ord.monogramDetails.style})
                      </p>
                    )}
                    {ord.giftWrapFee > 0 && (
                      <p className="text-amber-800 font-semibold">🎁 Gift Wrap Included • Note: "{ord.giftMessage}"</p>
                    )}
                    <p><strong>Total:</strong> ₹{ord.totalAmount.toLocaleString('en-IN')} via {ord.paymentMethod}</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* Tab 5: Categories */}
        {adminTab === 'categories' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <h3 className="text-lg font-serif font-bold text-stone-950">Categories</h3>
            <div className="flex gap-2 max-w-md">
              <input
                type="text"
                placeholder="New Category..."
                value={newCatInput}
                onChange={(e) => setNewCatInput(e.target.value)}
                className="flex-1 px-3 py-2 text-xs rounded-xl border border-stone-300"
              />
              <button
                onClick={() => {
                  onAddCategory(newCatInput);
                  setNewCatInput('');
                }}
                className="px-4 py-2 bg-stone-950 text-[#D4AF37] text-xs font-bold rounded-xl"
              >
                Add Category
              </button>
            </div>
            <div className="flex flex-wrap gap-2 pt-2">
              {categories.map((c) => (
                <div key={c} className="px-3 py-1.5 bg-stone-100 rounded-xl border text-xs font-semibold flex items-center gap-2">
                  <span>{c}</span>
                  {c !== 'All' && (
                    <button onClick={() => onDeleteCategory(c)} className="text-stone-400 hover:text-rose-600">
                      <X className="w-3.5 h-3.5" />
                    </button>
                  )}
                </div>
              ))}
            </div>
          </div>
        )}

        {/* Tab 6: Coupons */}
        {adminTab === 'coupons' && (
          <div className="bg-white rounded-2xl border border-stone-200 p-6 space-y-4">
            <h3 className="text-lg font-serif font-bold text-stone-950">Active Promo Coupons</h3>
            <div className="grid grid-cols-1 sm:grid-cols-3 gap-4">
              {coupons.map((cp) => (
                <div key={cp.code} className="p-4 rounded-2xl border border-stone-200 bg-stone-50 space-y-2">
                  <div className="flex justify-between items-center">
                    <span className="font-mono font-bold text-sm text-stone-900 bg-white px-2 py-0.5 rounded border border-stone-300">
                      {cp.code}
                    </span>
                    <span className="text-xs font-bold text-emerald-700">
                      {cp.type === 'percentage' ? `${cp.value}% OFF` : `₹${cp.value} OFF`}
                    </span>
                  </div>
                  <p className="text-xs text-stone-600">{cp.description}</p>
                  <p className="text-[10px] text-stone-400">Min Order: ₹{cp.minOrder}</p>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
}

function ProductFormModal({ product, categories, onClose, onSave }) {
  const [formData, setFormData] = useState({
    id: product ? product.id : '',
    name: product ? product.name : '',
    category: product ? product.category : categories[1] || 'Handbags',
    price: product ? product.price : 1499,
    mrp: product ? product.mrp : 2999,
    stock: product ? product.stock : 10,
    lowStockThreshold: product ? product.lowStockThreshold : 4,
    rating: product ? product.rating : 4.8,
    reviewsCount: product ? product.reviewsCount : 12,
    isFeatured: product ? product.isFeatured : false,
    isNewArrival: product ? product.isNewArrival : true,
    isActive: product ? product.isActive : true,
    dimensions: product ? product.dimensions || '30cm x 22cm x 10cm' : '30cm x 22cm x 10cm',
    material: product ? product.material || 'Full Grain Leather' : 'Full Grain Leather',
    weight: product ? product.weight || '650 grams' : '650 grams',
    strapType: product ? product.strapType || 'Adjustable Leather Strap' : 'Adjustable Leather Strap',
    laptopCompatibility: product ? product.laptopCompatibility || '11" Tablet' : '11" Tablet',
    fitsInsideText: product && product.fitsInside ? product.fitsInside.join(', ') : 'Smartphone, Wallet, Cosmetics, Keys',
    imagesText: product ? (product.images || []).join('\n') : 'https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80',
    colorsText: product ? (product.colors || []).join(', ') : 'Black, Tan, Brown',
    sizesText: product ? (product.sizes || []).join(', ') : 'Standard',
    description: product ? product.description : 'Handcrafted full grain leather with anti-rust fittings and multi-compartment dividers.'
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    const imgs = formData.imagesText.split('\n').map((s) => s.trim()).filter(Boolean);
    const cols = formData.colorsText.split(',').map((s) => s.trim()).filter(Boolean);
    const szs = formData.sizesText.split(',').map((s) => s.trim()).filter(Boolean);
    const fits = formData.fitsInsideText.split(',').map((s) => s.trim()).filter(Boolean);

    onSave({
      ...formData,
      price: Number(formData.price),
      mrp: Number(formData.mrp),
      stock: Number(formData.stock),
      lowStockThreshold: Number(formData.lowStockThreshold),
      rating: Number(formData.rating),
      reviewsCount: Number(formData.reviewsCount),
      images: imgs.length > 0 ? imgs : ['https://images.unsplash.com/photo-1584917865442-de89df76afd3?auto=format&fit=crop&w=900&q=80'],
      colors: cols,
      sizes: szs,
      fitsInside: fits
    });
  };

  return (
    <div className="fixed inset-0 z-50 overflow-y-auto bg-stone-950/70 backdrop-blur-sm flex items-center justify-center p-4">
      <div className="bg-white rounded-3xl max-w-2xl w-full p-6 space-y-4 shadow-2xl border border-stone-200">
        <div className="flex justify-between items-center border-b pb-3">
          <h3 className="text-base font-serif font-bold text-stone-950">
            {product ? `Edit Product: ${product.name}` : 'Add New Bag'}
          </h3>
          <button onClick={onClose} className="text-stone-400 hover:text-stone-700">
            <X className="w-5 h-5" />
          </button>
        </div>

        <form onSubmit={handleSubmit} className="space-y-3 text-xs max-h-[75vh] overflow-y-auto pr-1">
          <div>
            <label className="font-bold text-stone-700 block mb-1">Bag Name *</label>
            <input
              required
              type="text"
              value={formData.name}
              onChange={(e) => setFormData({ ...formData, name: e.target.value })}
              className="w-full px-3 py-2 border rounded-xl"
            />
          </div>

          <div className="grid grid-cols-2 sm:grid-cols-4 gap-3">
            <div>
              <label className="font-bold text-stone-700 block mb-1">Category</label>
              <select
                value={formData.category}
                onChange={(e) => setFormData({ ...formData, category: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl bg-white"
              >
                {categories.filter((c) => c !== 'All').map((c) => (
                  <option key={c} value={c}>{c}</option>
                ))}
              </select>
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">Selling Price (₹)</label>
              <input
                required
                type="number"
                value={formData.price}
                onChange={(e) => setFormData({ ...formData, price: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">MRP Price (₹)</label>
              <input
                required
                type="number"
                value={formData.mrp}
                onChange={(e) => setFormData({ ...formData, mrp: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">Stock Units</label>
              <input
                required
                type="number"
                value={formData.stock}
                onChange={(e) => setFormData({ ...formData, stock: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
          </div>

          <div className="grid grid-cols-2 gap-3">
            <div>
              <label className="font-bold text-stone-700 block mb-1">Material (e.g. Tuscan Leather)</label>
              <input
                type="text"
                value={formData.material}
                onChange={(e) => setFormData({ ...formData, material: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">Weight (e.g. 680g)</label>
              <input
                type="text"
                value={formData.weight}
                onChange={(e) => setFormData({ ...formData, weight: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
          </div>

          <div className="grid grid-cols-2 gap-3">
            <div>
              <label className="font-bold text-stone-700 block mb-1">Dimensions (e.g. 32cm x 24cm)</label>
              <input
                type="text"
                value={formData.dimensions}
                onChange={(e) => setFormData({ ...formData, dimensions: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">Laptop Fit (e.g. Up to 15.6")</label>
              <input
                type="text"
                value={formData.laptopCompatibility}
                onChange={(e) => setFormData({ ...formData, laptopCompatibility: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
          </div>

          <div>
            <label className="font-bold text-stone-700 block mb-1">Image URLs (one per line)</label>
            <textarea
              rows={3}
              value={formData.imagesText}
              onChange={(e) => setFormData({ ...formData, imagesText: e.target.value })}
              className="w-full px-3 py-2 border rounded-xl font-mono text-[10px]"
            />
          </div>

          <div className="grid grid-cols-2 gap-3">
            <div>
              <label className="font-bold text-stone-700 block mb-1">Colors (Comma separated)</label>
              <input
                type="text"
                value={formData.colorsText}
                onChange={(e) => setFormData({ ...formData, colorsText: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
            <div>
              <label className="font-bold text-stone-700 block mb-1">Sizes (Comma separated)</label>
              <input
                type="text"
                value={formData.sizesText}
                onChange={(e) => setFormData({ ...formData, sizesText: e.target.value })}
                className="w-full px-3 py-2 border rounded-xl"
              />
            </div>
          </div>

          <div>
            <label className="font-bold text-stone-700 block mb-1">Description</label>
            <textarea
              rows={3}
              value={formData.description}
              onChange={(e) => setFormData({ ...formData, description: e.target.value })}
              className="w-full px-3 py-2 border rounded-xl"
            />
          </div>

          <div className="flex gap-4 pt-1">
            <label className="flex items-center gap-1.5 cursor-pointer">
              <input
                type="checkbox"
                checked={formData.isFeatured}
                onChange={(e) => setFormData({ ...formData, isFeatured: e.target.checked })}
              />
              <span>Featured Bag</span>
            </label>
            <label className="flex items-center gap-1.5 cursor-pointer">
              <input
                type="checkbox"
                checked={formData.isNewArrival}
                onChange={(e) => setFormData({ ...formData, isNewArrival: e.target.checked })}
              />
              <span>New Arrival</span>
            </label>
          </div>

          <div className="flex justify-end gap-2 pt-3 border-t">
            <button type="button" onClick={onClose} className="px-4 py-2 border rounded-xl font-semibold">
              Cancel
            </button>
            <button type="submit" className="px-5 py-2 bg-stone-950 text-[#D4AF37] font-bold rounded-xl">
              Save Product
            </button>
          </div>
        </form>
      </div>
    </div>
  );
}
