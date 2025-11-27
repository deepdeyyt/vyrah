document.addEventListener("DOMContentLoaded", function () {
  gsap.registerPlugin(ScrollTrigger);

  ScrollTrigger.matchMedia({
    // Desktop version (min-width: 768px)
    "(min-width: 768px)": function () {
      // Animate [data-anim-vid]
      gsap.to("[data-anim-vid]", {
        paddingBottom: "20%",
        paddingLeft: "45%",
        ease: "none",
        scrollTrigger: {
          trigger: ".about_video-container",
          start: "top 85%",
          end: "bottom 55%",
          scrub: true,
        },
      });

      // Animate background container
      gsap.to(".about_video-container-bg", {
        opacity: "0",
        ease: "power2.inOut",
        scrollTrigger: {
          trigger: ".about_video-container",
          start: "top 85%",
          end: "bottom 55%",
          scrub: true,
        },
      });
    },

    // Mobile version (max-width: 767px)
    "(max-width: 767px)": function () {
      // Animate [data-anim-vid] for mobile
      gsap.to("[data-anim-vid]", {
        paddingBottom: "25%", // Adjusted value for mobile screens
        paddingLeft: "100%", // Adjusted value for mobile screens
        ease: "none",
        scrollTrigger: {
          trigger: ".about_video-container",
          start: "top 95%", // You may need to tweak these for mobile scrolling flow
          end: "bottom 65%",
          scrub: true,
        },
      });

      // Animate background container for mobile
      gsap.to(".about_video-container-bg", {
        opacity: "0", // Change if needed for mobile
        ease: "power2.inOut",
        scrollTrigger: {
          trigger: ".about_video-container",
          start: "top 95%",
          end: "bottom 65%",
          scrub: true,
        },
      });
    },
  });
});

// // Select the parent container and the initial element
// const container = document.querySelector(".frame_contain");
// const originalEl = document.querySelector(".frame_el");

// // Create 5 duplicates (resulting in 6 total)
// for (let i = 0; i < 8; i++) {
//   let clone = originalEl.cloneNode(true);
//   container.appendChild(clone);
// }

// // Create the infinite scaling loop for each .frame_el element
// gsap.utils.toArray(".frame_el").forEach((el, index) => {
//   // Create a timeline that repeats infinitely with a staggered delay
//   const tl = gsap.timeline({ repeat: -1, delay: index * 0.2 });

//   tl.fromTo(
//     el,
//     { scale: 0.6, opacity: 1 },
//     {
//       scale: 1,
//       duration: 1,
//       ease: "power1.inOut",
//       // Increase z-index when scaling up
//       onStart: () => {
//         el.style.zIndex = 10;
//       },
//     }
//   )
//     .to(el, { opacity: 0, duration: 0.5, ease: "power1.inOut" })
//     // Reset the element to its initial small state and lower its z-index
//     .set(el, { scale: 0.6, opacity: 0, zIndex: -1 })
//     .to(el, { opacity: 1, duration: 0.1, ease: "power1.inOut" });
// });

// Button duplication and hover animations
const btnDup = () => {
  document.querySelectorAll(".btn").forEach((btn) => {
    const originalText = btn.innerHTML;
    const wrapperDiv = document.createElement("div");
    wrapperDiv.classList.add("btn-wrapper");

    const createSpan = (text, additionalClass = "") => {
      const span = document.createElement("span");
      span.innerHTML = text;
      if (additionalClass) span.classList.add(additionalClass);
      return span;
    };

    wrapperDiv.append(
      createSpan(originalText),
      createSpan(originalText, "second")
    );
    btn.innerHTML = "";
    btn.appendChild(wrapperDiv);

    btn.addEventListener("mouseenter", () => {
      gsap.to(wrapperDiv.children, {
        duration: 0.4,
        y: "-100%",
        ease: "power1.out",
      });
    });

    btn.addEventListener("mouseleave", () => {
      gsap.to(wrapperDiv.children, {
        duration: 0.4,
        y: "0%",
        ease: "power2.out",
      });
    });
  });
};

btnDup();

function adjustGrid() {
  return new Promise((resolve) => {
    const transition = document.querySelector(".transition");

    // Get computed style of the grid and extract the number of columns
    const computedStyle = window.getComputedStyle(transition);
    const gridTemplateColumns = computedStyle.getPropertyValue(
      "grid-template-columns"
    );
    const columns = gridTemplateColumns.split(" ").length; // Count the number of columns

    const blockSize = window.innerWidth / columns;
    const rowsNeeded = Math.ceil(window.innerHeight / blockSize);

    // Update grid styles
    transition.style.gridTemplateRows = `repeat(${rowsNeeded}, ${blockSize}px)`;

    // Calculate the total number of blocks needed
    const totalBlocks = columns * rowsNeeded;

    // Clear existing blocks
    transition.innerHTML = "";

    // Generate blocks dynamically
    for (let i = 0; i < totalBlocks; i++) {
      const block = document.createElement("div");
      block.classList.add("transition-block");
      transition.appendChild(block);
    }

    // Resolve the Promise after grid creation is complete
    resolve();
  });
}

document.addEventListener("DOMContentLoaded", () => {
  adjustGrid().then(() => {
    let pageLoadTimeline = gsap.timeline({
      onStart: () => {
        gsap.set(".transition", { background: "transparent" });
      },
      onComplete: () => {
        gsap.set(".transition", { display: "none" });
      },
      defaults: {
        ease: "linear",
      },
    });

    // Play the timeline only after the grid is ready
    pageLoadTimeline.to(
      ".transition-block",
      {
        opacity: 0,
        duration: 0.1,
        stagger: { amount: 0.75, from: "random" },
      },
      0.5
    );
  });

  // Pre-process all valid links
  const validLinks = Array.from(document.querySelectorAll("a")).filter(
    (link) => {
      const href = link.getAttribute("href") || "";
      const hostname = new URL(link.href, window.location.origin).hostname;

      return (
        hostname === window.location.hostname && // Same domain
        !href.startsWith("#") && // Not an anchor link
        link.getAttribute("target") !== "_blank" && // Not opening in a new tab
        !link.hasAttribute("data-transition-prevent") // No 'data-transition-prevent' attribute
      );
    }
  );

  // Add event listeners to pre-processed valid links
  validLinks.forEach((link) => {
    link.addEventListener("click", (event) => {
      event.preventDefault();
      const destination = link.href;

      // Show loading grid with animation
      gsap.set(".transition", { display: "grid" });
      gsap.fromTo(
        ".transition-block",
        { autoAlpha: 0 },
        {
          autoAlpha: 1,
          duration: 0.001,
          ease: "linear",
          stagger: { amount: 0.5, from: "random" },
          onComplete: () => {
            window.location.href = destination;
          },
        }
      );
    });
  });

  window.addEventListener("pageshow", (event) => {
    if (event.persisted) {
      window.location.reload();
    }
  });

  window.addEventListener("resize", adjustGrid);
});

// // Open button click event: add the "is--active" class to ".m-nav_menu"
// document
//   .querySelector(".m-nav_open-btn")
//   .addEventListener("click", function () {
//     document.querySelector(".m-nav_menu").classList.add("is--active");
//   });

// // Close button click event: remove the "is--active" class from ".m-nav_menu"
// document
//   .querySelector(".m-nav_close-btn")
//   .addEventListener("click", function () {
//     document.querySelector(".m-nav_menu").classList.remove("is--active");
//   });

document.addEventListener("DOMContentLoaded", function () {
  // Register GSAP plugins
  gsap.registerPlugin(ScrollTrigger);

  // Efficiently select all headings with [data-anim-h]
  let headings = gsap.utils.toArray("[data-anim-h]");

  headings.forEach((heading) => {
    // Ensure SplitType is applied only once
    if (!heading.dataset.splitApplied) {
      let typeSplit = new SplitType(heading, {
        types: "words",
        tagName: "span",
      });
      heading.dataset.splitApplied = true; // Prevent multiple initializations

      let tl = gsap.timeline({
        scrollTrigger: {
          trigger: ".scroll-wrap",
          start: "5% center",
          end: "bottom bottom",
          toggleActions: "play none none none",
        },
      });

      tl.from(typeSplit.words, {
        y: "100%",
        opacity: 0,
        rotationZ: 3,
        filter: "blur(5px)",
        duration: 1,
        ease: "power2.out",
        stagger: 0.05,
      });
    }
  });
});

// // Section Headings Animate In
// document.addEventListener("DOMContentLoaded", () => {
//   gsap.utils.toArray("[sec-heading]").forEach((heading) => {
//     let typeSplit = new SplitType(heading, {
//       types: "lines, words, chars",
//       tagName: "span",
//     });

//     gsap.from(heading.querySelectorAll(".char"), {
//       y: "100%",
//       opacity: 0,
//       rotationZ: 4,
//       duration: 0.5,
//       ease: "power2.out",
//       stagger: 0.04,
//       scrollTrigger: {
//         trigger: heading,
//         start: "top 80%",
//       },
//     });
//   });
// });

// Paragraph Opacity Scrub
if (document.querySelector("[opscrub]")) {
  let typeSplit = new SplitType("[opscrub]", {
    types: "words, chars",
    tagName: "span",
  });

  gsap.from(typeSplit.chars, {
    opacity: 0.2,
    duration: 1,
    stagger: 0.2,
    ease: "power2.out",
    scrollTrigger: {
      trigger: "[opscrub]",
      start: "top 90%",
      end: "bottom 50%",
      scrub: true,
    },
  });
}

// Databox fade in
gsap.registerPlugin(ScrollTrigger);

gsap.from(".about-stat", {
  opacity: 0,
  yPercent: 50,
  duration: 0.8,
  ease: "power2.out",
  stagger: 0.3,
  scrollTrigger: {
    trigger: ".about-stat",
    start: "top 80%",
    end: "top 50%",
    toggleActions: "play none none reverse",
  },
});

// Databox fade in
gsap.registerPlugin(ScrollTrigger);

gsap.from("[data-anim-fu]", {
  opacity: 0,
  yPercent: 30,
  duration: 0.8,
  ease: "power2.out",
  stagger: 0.2,
  scrollTrigger: {
    trigger: "[data-anim-fu]",
    start: "top 90%",
    end: "top 50%",
    toggleActions: "play none none reverse",
  },
});

document.addEventListener("DOMContentLoaded", () => {
  const navInner = document.querySelector(".nav_c-inner");
  const navLeft = document.querySelector(".nav_content.is--left");
  const navRight = document.querySelector(".nav_content.is--right");
  const navItems = document.querySelectorAll(".nav_content.is--items > *");
  const body = document.body;

  // GSAP timeline for opening
  const navTimeline = gsap.timeline({ paused: true });

  navTimeline
    .to({}, { duration: 0.8 }) // Delay for .is--active
    .fromTo(
      navLeft,
      { opacity: 0, y: "2rem" },
      { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }
    )
    .fromTo(
      navRight,
      { opacity: 0, y: "2rem" },
      { opacity: 1, y: 0, duration: 0.5, ease: "power2.out" },
      ">-0.25"
    )
    .fromTo(
      navItems,
      { opacity: 0, y: "2rem" },
      {
        opacity: 1,
        y: 0,
        duration: 0.4,
        ease: "power2.out",
        stagger: 0.08,
      },
      ">-0.4"
    );

  function lockBodyScroll() {
    body.style.overflow = "hidden";
    body.style.height = "100vh";
    body.style.position = "fixed";
    body.style.width = "100%";
  }
  function unlockBodyScroll() {
    body.style.overflow = "";
    body.style.height = "";
    body.style.position = "";
    body.style.width = "";
  }

  // Fade out everything on close (opacity only)
  function fadeOutNavContent() {
    gsap.to([navLeft, navRight, ...navItems], {
      opacity: 0,
      duration: 0.35,
      ease: "power2.inOut",
      onComplete: resetNavContent, // Reset for next open (now hidden)
    });
  }

  // Reset all items to closed state, ready for timeline on next open (reset y after fade)
  function resetNavContent() {
    gsap.set(navLeft, { opacity: 0, y: "2rem" });
    gsap.set(navRight, { opacity: 0, y: "2rem" });
    gsap.set(navItems, { opacity: 0, y: "2rem" });
    navTimeline.pause(0); // Reset timeline for next open
  }

  // Open nav
  document.querySelectorAll('[data-nav-toggle="open"]').forEach((btn) => {
    btn.addEventListener("click", () => {
      navInner.classList.add("is--active");
      lockBodyScroll();
      navTimeline.restart();
    });
  });

  // Close nav
  document.querySelectorAll('[data-nav-toggle="close"]').forEach((btn) => {
    btn.addEventListener("click", () => {
      navInner.classList.remove("is--active");
      unlockBodyScroll();
      fadeOutNavContent();
    });
  });

  // (Optional) Reset content if nav is closed on page load
  if (!navInner.classList.contains("is--active")) {
    resetNavContent();
  }
});

// Note: The Javascript is optional. Read the documentation below how to use the CSS Only version.

function initCSSMarquee() {
  const pixelsPerSecond = 75; // Set the marquee speed (pixels per second)
  const marquees = document.querySelectorAll("[data-css-marquee]");

  // Duplicate each [data-css-marquee-list] element inside its container
  marquees.forEach((marquee) => {
    marquee.querySelectorAll("[data-css-marquee-list]").forEach((list) => {
      const duplicate = list.cloneNode(true);
      marquee.appendChild(duplicate);
    });
  });

  // Create an IntersectionObserver to check if the marquee container is in view
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        entry.target
          .querySelectorAll("[data-css-marquee-list]")
          .forEach(
            (list) =>
              (list.style.animationPlayState = entry.isIntersecting
                ? "running"
                : "paused")
          );
      });
    },
    { threshold: 0 }
  );

  // Calculate the width and set the animation duration accordingly
  marquees.forEach((marquee) => {
    marquee.querySelectorAll("[data-css-marquee-list]").forEach((list) => {
      list.style.animationDuration = list.offsetWidth / pixelsPerSecond + "s";
      list.style.animationPlayState = "paused";
    });
    observer.observe(marquee);
  });
}

// Initialize CSS Marquee
document.addEventListener("DOMContentLoaded", function () {
  initCSSMarquee();
});

document.querySelectorAll(".sp_card").forEach((card) => {
  const blocks = Array.from(card.querySelectorAll(".adv-card_block"));
  const iconWrap = card.querySelector(".adv-card_ico-wrap");

  // Shuffle utility function
  function shuffle(array) {
    return array
      .map((value) => ({ value, sort: Math.random() }))
      .sort((a, b) => a.sort - b.sort)
      .map(({ value }) => value);
  }

  // Ensure everything is hidden on load
  blocks.forEach((block) => gsap.set(block, { opacity: 0 }));
  gsap.set(iconWrap, { opacity: 0 });

  card.addEventListener("mouseenter", () => {
    const shuffledBlocks = shuffle(blocks);

    shuffledBlocks.forEach((block, i) => {
      const finalOpacity = parseFloat(block.dataset.opacity) || 1;

      gsap.to(block, {
        opacity: finalOpacity,
        duration: 0.2,
        ease: "power1.out",
        delay: i * 0.015, // slightly faster stagger
        overwrite: true,
      });
    });

    gsap.to(iconWrap, {
      opacity: 1,
      duration: 0.3,
      delay: 0.15,
      ease: "power1.out",
      overwrite: true,
    });
  });

  card.addEventListener("mouseleave", () => {
    gsap.to([...blocks, iconWrap], {
      opacity: 0,
      duration: 0.2,
      overwrite: true,
    });
  });
});

document.addEventListener("DOMContentLoaded", () => {
  const updateBodyScroll = () => {
    const isAnyModalOpen = document.querySelector(".adv_modal-wrap.is--open");
    document.body.style.overflow = isAnyModalOpen ? "hidden" : "";
  };

  // Open modal
  document.querySelectorAll("[data-adv-trigger]").forEach((trigger) => {
    trigger.addEventListener("click", () => {
      const value = trigger.getAttribute("data-adv-trigger");
      const modal = document.querySelector(
        `.adv_modal-wrap[data-adv-modal="${value}"]`
      );
      if (modal) {
        modal.classList.add("is--open");
        updateBodyScroll();
      }
    });
  });

  // Close all modals via close element
  document.querySelectorAll("[data-adv-close]").forEach((closer) => {
    closer.addEventListener("click", () => {
      document.querySelectorAll(".adv_modal-wrap.is--open").forEach((modal) => {
        modal.classList.remove("is--open");
      });
      updateBodyScroll();
    });
  });

  // Close all modals on Escape key
  document.addEventListener("keydown", (e) => {
    if (e.key === "Escape" || e.key === "Esc") {
      document.querySelectorAll(".adv_modal-wrap.is--open").forEach((modal) => {
        modal.classList.remove("is--open");
      });
      updateBodyScroll();
    }
  });

  // Close all modals when clicking outside .adv-modal_inner
  document.querySelectorAll(".adv_modal-wrap").forEach((modal) => {
    modal.addEventListener("click", (e) => {
      const inner = modal.querySelector(".adv-modal_inner");
      if (inner && !inner.contains(e.target)) {
        modal.classList.remove("is--open");
        updateBodyScroll();
      }
    });
  });
});
