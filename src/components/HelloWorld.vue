<script setup lang="ts">
import {inject, ref} from "vue";

const phantom: any = inject("phantom");
const publicWalletAddress = ref("");

const connectPhantom = async () => {
  if (phantom) {
    const response = await phantom.connect();
    publicWalletAddress.value = response.publicKey.toString();
    console.log('Connected with Public Key:', response)
  }
}

</script>

<template>
  <div id="main-container">
    <template v-if="phantom && !publicWalletAddress">
      <button
          class="btn-mg"
          @click="connectPhantom"
      >
        CONNECT WALLET
      </button>
    </template>

    <template v-if="publicWalletAddress">
      <div>
        <p class="text-white-mg">
          Welcome to the Solana network, <br/>
          <strong>{{ publicWalletAddress }}</strong>
        </p>
        <div >
          <img src="static/images/welcome.gif" alt="welcome gif" />
        </div>
      </div>
    </template>

    <template v-if="phantom === null">
      <div class="no-phantom-wallet-container">
        <div >
          <div class="lds-dual-ring"></div>
          <p>Checking ...</p>
        </div>
        <a
            href="https://phantom.app/"
            target="_blank"
        >
          You don't have a Phantom wallet ! Get one there !
        </a>
      </div>
    </template>
  </div>



  <div id="footer-container">
    <a
        href="https://github.com/Foetus6907/vuejs3-solana-boilerplate"
        target="_blank"
        class="github-link"
    >
      <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="currentColor"
      >
        <path
            d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
        />
      </svg>
      <p>This project is OpenSource</p>
    </a>
  </div>
</template>

<style scoped>
#main-container {
  width: 100%;
  height: 90%;
  display: flex;
  justify-content: center;
  align-items: center;
}

#footer-container {
  width: 100%;
  height: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.btn-mg {
  border-radius: 5px;
  background-color: #4f46e5;
  color: white;
  font-weight: bolder;
  line-height: 1.5em;
  font-size: 20px;
  border: none;
  padding: 10px;
}

.github-link {
  color: white;
  text-decoration: none;
  font-weight: bolder;
}
.text-white-mg {
  color: white
}
.no-phantom-wallet-container {
  color: white;
  font-weight: bolder;
}
.no-phantom-wallet-container a {
  color: #4f46e5;
  font-weight: bolder;
  text-decoration: none;
}

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
