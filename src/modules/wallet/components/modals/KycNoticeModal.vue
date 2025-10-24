<template>
  <div class="modal-dialog wallet-modal" role="document">
    <div class="modal-content">
      <div class="modal-body">
        <div>
          <h3 class="text-capitalize">Security Notice</h3>
          <div class="security-notice">
            <p>
              To use our service, you need to complete a Know Your Customer
              (KYC) check, which is a process for verifying your identity to
              prevent fraud and financial crimes like money laundering.
            </p>
            <div class="text-center">
              <button
                type="button"
                class="btn btn-primary btn-block py-2"
                @click="goToKyc"
              >
                Complete KYC
              </button>
              <button
                type="button"
                class="btn btn-danger btn-block py-2"
                @click="handleLogout"
              >
                Logout
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import handleLogout from "~/mixins/handleLogout";

export default {
  name: "KycNoticeModal",
  mixins: [handleLogout],
  emits: ["close"],
  methods: {
    goToKyc() {
      this.$router.push("/kyc");
      this.$modal.close();
    },
  },
};
</script>

<style scoped>
.security-notice {
  font-size: 14px;
  max-width: 420px;
  margin: 0 auto;
  padding: 0 40px;
}

p {
  margin-top: 15px;
}

.btn-block {
  width: 180px;
  margin: 10px auto 0 auto;
}

@media screen and (max-width: 600px) {
  .security-notice {
    padding: 0;
  }
}
</style>
