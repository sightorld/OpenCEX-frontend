<template>
  <Teleport to="body">
    <div v-if="visible" class="kyc-modal-overlay">
      <div class="kyc-modal-container">
        <div class="kyc-modal-content">
          <h3 class="kyc-modal-title">Security Notice</h3>
          <div class="kyc-modal-body">
            <p>
              To use our service, you need to complete a Know Your Customer
              (KYC) check, which is a process for verifying your identity to
              prevent fraud and financial crimes like money laundering.
            </p>
            <div class="kyc-modal-actions">
              <button
                type="button"
                class="btn btn-primary kyc-modal-btn"
                @click="goToKyc"
              >
                Complete KYC
              </button>
              <button
                type="button"
                class="btn btn-danger kyc-modal-btn"
                @click="handleLogout"
              >
                Logout
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script>
import handleLogout from "~/mixins/handleLogout";

export default {
  name: "KycTeleportModal",
  mixins: [handleLogout],
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
  },
  emits: ["close"],
  mounted() {
    document.body.style.overflow = "hidden";
  },
  beforeUnmount() {
    document.body.style.overflow = "";
  },
  methods: {
    goToKyc() {
      this.$router.push("/kyc");
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.kyc-modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.kyc-modal-container {
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow: auto;
}

.kyc-modal-content {
  padding: 30px;
}

.kyc-modal-title {
  font-size: 1.5rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 20px;
  color: #2b395b;
}

.kyc-modal-body {
  text-align: center;
}

.kyc-modal-body p {
  font-size: 14px;
  line-height: 1.5;
  margin-bottom: 30px;
  color: #333;
}

.kyc-modal-actions {
  display: flex;
  flex-direction: column;
  gap: 15px;
  align-items: center;
}

.kyc-modal-btn {
  width: 180px;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-primary {
  background: var(--theme-primary-color, #007bff) !important;
  color: white;
}

.btn-primary:hover {
  opacity: 0.9;
}

.btn-danger {
  background: #dc3545 !important;
  color: white;
}

.btn-danger:hover {
  background: #c82333;
}

@media screen and (max-width: 600px) {
  .kyc-modal-content {
    padding: 20px;
  }
  .kyc-modal-btn {
    width: 100%;
  }
}
</style>
