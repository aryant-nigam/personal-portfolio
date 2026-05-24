<template>
  <section
    id="contact"
    class="glass-section text-white py-5 position-relative z-1"
    style="border-top-left-radius: 40px; border-top-right-radius: 40px; margin-top: 5rem;"
  >
    <div class="container py-5">
      <div class="row gy-5 align-items-center">

        <!-- Left Side -->
        <div class="col-lg-5 mb-4 mb-lg-0 text-md-start text-center">
          <h2
            class="display-3 fw-bold mb-4 tracking-tight"
            style="line-height: 1.05;"
          >
            Let's connect.<br />
            I build things that matter.
          </h2>

          <p
            class="text-lighter mb-4"
            style="font-size: 1.05rem; line-height: 1.75; max-width: 38rem;"
          >
            If you have an idea, a product challenge, or want to collaborate on
            something meaningful, send me a note. I’ll reply personally and help
            you move forward.
          </p>
        </div>

        <!-- Right Side -->
        <div class="col-lg-7">
          <div
            class="contact-card p-4 p-md-5 rounded-4 bg-black bg-opacity-50 shadow-lg h-100"
          >
            <p class="text-lighter mb-4 text-center">
              Reach me directly using one of the
              buttons below.
            </p>

            <div class="d-grid gap-3">
              <!-- Email -->
              <a
                :href="gmailEmbeddedMessage"
                aria-label="Send email to Aryant"
                class="btn btn-outline-light btn-lg rounded-4 text-white d-flex align-items-center justify-content-center gap-3 py-3 w-100 contact-btn"
              >
                <SvgIcon name="MailIcon" size="24" class="icon" />
                <span class="fw-semibold">Email me</span>
              </a>

              <!-- Phone / WhatsApp -->
              <div class="position-relative">
                <button
                  ref="phoneToggle"
                  @click="openWhatsappModal"
                  aria-haspopup="true"
                  aria-label="Contact options for Aryant"
                  type="button"
                  class="btn btn-light btn-lg rounded-4 text-dark d-flex align-items-center justify-content-center gap-3 py-3 w-100 contact-btn"
                >
                  <SvgIcon name="Whatsapp" size="24" class="icon" />
                  <span class="fw-semibold">+91 83186 41872</span>
                </button>

                <teleport to="body">
                  <div v-if="showWhatsappModal">

                    <!-- Backdrop -->
                    <div
                      class="custom-backdrop"
                      @click="closeWhatsappModal"
                    ></div>

                    <!-- Modal -->
                    <div
                      class="modal show d-block custom-modal-wrapper"
                      tabindex="-1"
                      role="dialog"
                      aria-modal="true"
                      @click.self="closeWhatsappModal"
                    >
                      <div
                        class="modal-dialog modal-dialog-centered"
                        role="document"
                      >
                        <div class="modal-content rounded-4 modal-black">

                          <!-- Header -->
                          <div
                            class="modal-header border-0 px-4 pt-4 pb-0"
                          >
                            <div>
                              <h5 class="modal-title text-white">
                                Contact on WhatsApp
                              </h5>

                              <p class="text-white-50 mb-0">
                                Choose how you'd like to reach me.
                              </p>
                            </div>

                            <button
                              type="button"
                              class="btn-close btn-close-white"
                              aria-label="Close"
                              @click="closeWhatsappModal"
                            ></button>
                          </div>

                          <!-- Body -->
                          <div class="modal-body px-4 pb-4 pt-3">
                            <div class="d-grid gap-3">

                              <!-- WhatsApp -->
                              <a
                                :href="whatsappEmbeddedMessage"
                                target="_blank"
                                rel="noopener noreferrer"
                                @click="closeWhatsappModal"
                                class="btn btn-outline-light btn-lg rounded-4 d-flex align-items-center justify-content-center gap-3 py-3"
                              >
                                <SvgIcon
                                  name="Whatsapp"
                                  size="24"
                                  class="icon"
                                />

                                <span class="fw-semibold">
                                  Message on WhatsApp
                                </span>
                              </a>

                              <!-- Call -->
                              <a
                                href="tel:+918318641872"
                                @click="closeWhatsappModal"
                                class="btn btn-outline-light btn-lg rounded-4 d-flex align-items-center justify-content-center gap-3 py-3"
                              >
                                <SvgIcon
                                  name="PhoneCallIcon"
                                  size="24"
                                  class="icon"
                                />

                                <span class="fw-semibold">
                                  Call +91 83186 41872
                                </span>
                              </a>

                            </div>
                          </div>

                        </div>
                      </div>
                    </div>

                  </div>
                </teleport>
              </div>
            </div>

            <p class="text-lighter small mt-4 mb-0 text-center">
              I usually respond within one business day.*
            </p>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
import SvgIcon from './SvgIcon.vue';

export default {
  name: 'Contact',

  components: {
    SvgIcon
  },

  data() {
    return {
      showWhatsappModal: false,
      showWhatsappModal: false,
      gmailSubject: import.meta.env.VITE_GMAIL_SUBJECT,
      gmailMessage: import.meta.env.VITE_GMAIL_MESSAGE,
      whatsappMessage: import.meta.env.VITE_WHATSAPP_MESSAGE 
    };
  },
  mounted() {
    console.log('Gmail Subject:', this.gmailSubject);
  },
  computed: {
    gmailEmbeddedMessage() {
      return `mailto:aryantnigam@gmail.com?subject=${this.gmailSubject}&body=${this.gmailMessage}`;
    },
    whatsappEmbeddedMessage() {
      return `https://wa.me/918318641872?text=${this.whatsappMessage}`;
    }
  },

  watch: {
    showWhatsappModal(value) {
      document.body.style.overflow = value ? 'hidden' : '';
    }
  },

  methods: {
    openWhatsappModal() {
      this.showWhatsappModal = true;
    },

    closeWhatsappModal() {
      this.showWhatsappModal = false;
    }
  },

  beforeUnmount() {
    document.body.style.overflow = '';
  }
};
</script>

<style scoped>
.glass-section {
  background: rgba(10, 10, 10, 0.65) !important;

  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);

  border-top: 1px solid rgba(255, 255, 255, 0.1);

  box-shadow: 0 -10px 40px rgba(0, 0, 0, 0.1);
}

.tracking-tight {
  letter-spacing: -0.02em;
}

.btn .icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.contact-card {
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
}

.contact-btn {
  transition:
    transform 0.18s ease,
    box-shadow 0.18s ease,
    background-color 0.18s ease;
}

.contact-btn:hover {
  transform: translateY(-2px);

  box-shadow: 0 14px 30px rgba(0, 0, 0, 0.18);
}

.btn-outline-light.contact-btn:hover,
.btn-outline-light.contact-btn:focus {
  background-color: rgba(255, 255, 255, 0.12) !important;

  color: #fff !important;

  border-color: rgba(255, 255, 255, 0.24) !important;
}

/* =========================
   BACKDROP
========================= */

.custom-backdrop {
  position: fixed;
  inset: 0;

  z-index: 1040;

  background: rgba(255, 255, 255, 0.03);

  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);

  transform: translateZ(0);
  will-change: backdrop-filter;
}

/* =========================
   MODAL
========================= */

.custom-modal-wrapper {
  z-index: 1050;

  transform: translateZ(0);
}

.modal-black {
  background: rgba(5, 6, 9, 0.92);

  border: 1px solid rgba(255, 255, 255, 0.08);

  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.45);
}

.modal-header .btn-close {
  filter: invert(1) opacity(0.8);
}

.text-lighter{
  color: rgba(255, 255, 255, 0.6) !important;
}
</style>