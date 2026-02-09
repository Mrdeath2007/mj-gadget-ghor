import { Link } from "react-router-dom";
import { ArrowRight, Truck, Shield, Headphones } from "lucide-react";
import { motion } from "framer-motion";
import Header from "@/components/Header";
import Footer from "@/components/Footer";
import ProductCard from "@/components/ProductCard";
import AnimatedSection from "@/components/AnimatedSection";
import { useLanguage } from "@/context/LanguageContext";
import { products } from "@/data/products";
import heroBanner from "@/assets/hero-banner.jpg";

const bestSellers = products.filter((p) => p.badge === "Best Seller" || p.badge === "Popular" || p.badge === "Hot").slice(0, 4);
const newArrivals = products.filter((p) => p.badge === "New" || !p.badge).slice(0, 4);
const deals = products.filter((p) => p.originalPrice).slice(0, 3);

const Index = () => {
  const { t } = useLanguage();

  return (
    <div className="min-h-screen bg-background">
      <Header />

      {/* Hero */}
      <section className="relative pt-16 overflow-hidden">
        <div className="section-padding py-20 md:py-28 grid grid-cols-1 lg:grid-cols-2 gap-10 items-center">
          <motion.div
            initial={{ opacity: 0, x: -40 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ duration: 0.7 }}
          >
            <p className="text-primary font-semibold text-sm uppercase tracking-widest mb-4">
              {t("Premium Tech Accessories", "প্রিমিয়াম টেক এক্সেসরিজ")}
            </p>
            <h1 className="text-5xl md:text-7xl font-bold text-foreground leading-[1.05] mb-6">
              {t("Upgrade Your", "আপগ্রেড করুন আপনার")}<br />
              <span className="text-gradient">{t("Tech Life", "টেক লাইফ")}</span>
            </h1>
            <p className="text-lg text-muted-foreground max-w-md mb-8 leading-relaxed">
              {t(
                "Discover premium cases, chargers, cables, and accessories — all at the best prices in Bangladesh.",
                "প্রিমিয়াম কেস, চার্জার, ক্যাবল এবং এক্সেসরিজ আবিষ্কার করুন — বাংলাদেশের সেরা দামে।"
              )}
            </p>
            <div className="flex flex-wrap gap-3">
              <Link
                to="/shop"
                className="inline-flex items-center gap-2 bg-foreground text-background font-semibold px-8 py-3.5 rounded-full hover:bg-primary transition-colors duration-300"
              >
                {t("Shop Now", "এখনই কিনুন")} <ArrowRight className="w-4 h-4" />
              </Link>
              <Link
                to="/about"
                className="inline-flex items-center gap-2 border border-border text-foreground font-semibold px-8 py-3.5 rounded-full hover:bg-secondary transition-colors duration-300"
              >
                {t("Learn More", "আরও জানুন")}
              </Link>
            </div>
          </motion.div>

          <motion.div
            initial={{ opacity: 0, scale: 0.9 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.7, delay: 0.2 }}
            className="relative"
          >
            <div className="rounded-3xl overflow-hidden shadow-elevated">
              <img src={heroBanner} alt="Tech accessories" className="w-full h-auto" />
            </div>
          </motion.div>
        </div>
      </section>

      {/* Trust Bar */}
      <section className="section-padding py-8 border-y border-border">
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {[
            { icon: Truck, label: t("Fast Delivery", "দ্রুত ডেলিভারি"), sub: t("All over Bangladesh", "সারা বাংলাদেশে") },
            { icon: Shield, label: t("Quality Guarantee", "গুণমান নিশ্চিত"), sub: t("Tested products only", "শুধুমাত্র পরীক্ষিত পণ্য") },
            { icon: Headphones, label: t("24/7 Support", "২৪/৭ সাপোর্ট"), sub: t("Always here to help", "সবসময় সাহায্যে আছি") },
          ].map((item) => (
            <div key={item.label} className="flex items-center gap-3 justify-center">
              <item.icon className="w-5 h-5 text-primary" />
              <div>
                <p className="text-sm font-semibold text-foreground">{item.label}</p>
                <p className="text-xs text-muted-foreground">{item.sub}</p>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* Best Sellers */}
      <section className="section-padding py-16 md:py-24">
        <AnimatedSection>
          <div className="flex items-end justify-between mb-10">
            <div>
              <p className="text-primary font-semibold text-sm uppercase tracking-wider mb-1">{t("Top Picks", "সেরা পছন্দ")}</p>
              <h2 className="text-3xl md:text-4xl font-bold text-foreground">{t("Best Sellers", "বেস্ট সেলার")}</h2>
            </div>
            <Link to="/shop" className="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors flex items-center gap-1">
              {t("View All", "সব দেখুন")} <ArrowRight className="w-4 h-4" />
            </Link>
          </div>
        </AnimatedSection>
        <div className="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-6">
          {bestSellers.map((p, i) => (
            <ProductCard key={p.id} product={p} index={i} />
          ))}
        </div>
      </section>

      {/* Featured Banner */}
      <section className="section-padding py-16">
        <AnimatedSection>
          <div className="relative bg-foreground text-background rounded-3xl overflow-hidden p-10 md:p-16">
            <div className="relative z-10 max-w-lg">
              <p className="text-primary font-semibold text-sm uppercase tracking-wider mb-3">{t("Special Offer", "বিশেষ অফার")}</p>
              <h2 className="text-3xl md:text-5xl font-bold mb-4 leading-tight">{t("Up to 30% Off on Bundles", "বান্ডেলে ৩০% পর্যন্ত ছাড়")}</h2>
              <p className="text-background/70 mb-6">
                {t(
                  "Get the best deals when you buy together. Premium cables, chargers, and cases — bundled for less.",
                  "একসাথে কিনলে সেরা ডিল পান। প্রিমিয়াম ক্যাবল, চার্জার এবং কেস — কম দামে বান্ডেল।"
                )}
              </p>
              <Link
                to="/deals"
                className="inline-flex items-center gap-2 bg-primary text-primary-foreground font-semibold px-8 py-3.5 rounded-full hover:opacity-90 transition-opacity"
              >
                {t("Shop Deals", "ডিল দেখুন")} <ArrowRight className="w-4 h-4" />
              </Link>
            </div>
            <div className="absolute top-0 right-0 w-1/2 h-full opacity-10">
              <div className="w-full h-full" style={{ background: "var(--hero-gradient)" }} />
            </div>
          </div>
        </AnimatedSection>
      </section>

      {/* New Arrivals */}
      <section className="section-padding py-16 md:py-24">
        <AnimatedSection>
          <div className="flex items-end justify-between mb-10">
            <div>
              <p className="text-primary font-semibold text-sm uppercase tracking-wider mb-1">{t("Just Arrived", "সদ্য এসেছে")}</p>
              <h2 className="text-3xl md:text-4xl font-bold text-foreground">{t("New Arrivals", "নতুন আগমন")}</h2>
            </div>
            <Link to="/shop" className="text-sm font-medium text-muted-foreground hover:text-foreground transition-colors flex items-center gap-1">
              {t("View All", "সব দেখুন")} <ArrowRight className="w-4 h-4" />
            </Link>
          </div>
        </AnimatedSection>
        <div className="grid grid-cols-2 md:grid-cols-4 gap-4 md:gap-6">
          {newArrivals.map((p, i) => (
            <ProductCard key={p.id} product={p} index={i} />
          ))}
        </div>
      </section>

      {/* Deals Row */}
      <section className="section-padding py-16 surface-dim">
        <AnimatedSection>
          <div className="text-center mb-10">
            <p className="text-primary font-semibold text-sm uppercase tracking-wider mb-1">{t("Limited Time", "সীমিত সময়")}</p>
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">{t("Today's Deals", "আজকের ডিল")}</h2>
          </div>
        </AnimatedSection>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
          {deals.map((product, i) => (
            <AnimatedSection key={product.id} delay={i * 0.1}>
              <Link to={`/product/${product.id}`} className="group block bg-card rounded-2xl overflow-hidden shadow-soft hover:shadow-elevated transition-all duration-500">
                <div className="aspect-[4/3] overflow-hidden bg-secondary">
                  <img src={product.image} alt={product.name} className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" />
                </div>
                <div className="p-5">
                  <h3 className="font-semibold text-foreground mb-1">{t(product.name, product.nameBn)}</h3>
                  <div className="flex items-center gap-2">
                    <span className="text-lg font-bold text-primary">৳{product.price}</span>
                    <span className="text-sm text-muted-foreground line-through">৳{product.originalPrice}</span>
                    <span className="text-xs font-semibold bg-primary/10 text-primary px-2 py-0.5 rounded-full">
                      {Math.round(((product.originalPrice! - product.price) / product.originalPrice!) * 100)}% OFF
                    </span>
                  </div>
                </div>
              </Link>
            </AnimatedSection>
          ))}
        </div>
      </section>

      {/* CTA */}
      <section className="section-padding py-20 md:py-28 text-center">
        <AnimatedSection>
          <h2 className="text-3xl md:text-5xl font-bold text-foreground mb-4">{t("Ready to upgrade?", "আপগ্রেড করতে প্রস্তুত?")}</h2>
          <p className="text-muted-foreground text-lg mb-8 max-w-md mx-auto">
            {t("Browse our full collection of premium tech accessories.", "আমাদের প্রিমিয়াম টেক এক্সেসরিজের সম্পূর্ণ কালেকশন ব্রাউজ করুন।")}
          </p>
          <Link
            to="/shop"
            className="inline-flex items-center gap-2 bg-foreground text-background font-semibold px-10 py-4 rounded-full hover:bg-primary transition-colors duration-300 text-lg"
          >
            {t("Explore Shop", "শপ দেখুন")} <ArrowRight className="w-5 h-5" />
          </Link>
        </AnimatedSection>
      </section>

      <Footer />
    </div>
  );
};

export default Index;
