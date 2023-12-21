<template>
  <div class="mx-auto max-w-4xl py-40 flex items-center justify-center">
    <div class="w-full px-4">
      <div class="p-8 bg-white rounded-xl">
        <form action="">
          <div class="flex flex-wrap -mx-4 mb-8 items-center">
            <div class="flex flex-wrap mb-6 -m-2.5 w-full px-4 mb-4">
              <div class="w-auto p-2 mr-8" v-for="subType of types">
                <div class="flex items-center">
                  <input
                    type="radio"
                    :id="subType.value"
                    v-model="type"
                    :value="subType.value"
                    class="w-5 h-5 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
                  />
                  <label :for="subType.value" class="pl-2"
                    >Use {{ subType.name }}</label
                  >
                </div>
              </div>
            </div>

            <div class="w-full px-4 mb-4" v-if="type !== 'usdt'">
              <label class="block mb-1 text-md font-medium" for=""
                >Network</label
              >
              <div
                class="flex h-11 bg-gray-50 bg-opacity-40 border border-gray-200 rounded-md"
              >
                <select
                  v-model="chain"
                  class="text-gray-900 text-sm rounded-lg block w-full p-2.5 outline-none"
                  name="chainName"
                >
                  <option value="goerli">Goerli</option>
                  <option value="polygon">Polygon</option>
                  <option value="bsc">Binance Smart Chain</option>
                </select>
              </div>
            </div>

            <div class="w-full px-4 mb-4" v-if="type === 'token'">
              <label class="block mb-1 text-md font-medium" for=""
                >Token Address</label
              >
              <input
                class="py-2 px-4 h-11 w-full text-gray-500 placeholder-gray-500 bg-gray-50 bg-opacity-40 border border-gray-200 focus:border-yellowGreen-500 rounded-lg outline-none ring ring-transparent focus:ring-yellowGreen-500"
                type="text"
                placeholder="Token Address"
                v-model="receiver"
              />
            </div>
            <div class="w-full px-4 mb-4">
              <label class="block mb-1 text-md font-medium" for=""
                >Receiver Address</label
              >
              <input
                class="py-2 px-4 h-11 w-full text-gray-500 placeholder-gray-500 bg-gray-50 bg-opacity-40 border border-gray-200 focus:border-yellowGreen-500 rounded-lg outline-none ring ring-transparent focus:ring-yellowGreen-500"
                type="text"
                placeholder="Receiver Address"
                v-model="receiver"
              />
            </div>
            <div class="w-full px-4 mb-4">
              <label class="block mb-1 text-md font-medium" for=""
                >Cost Per Day</label
              >
              <input
                class="py-2 px-4 h-11 w-full text-gray-500 placeholder-gray-500 bg-gray-50 bg-opacity-40 border border-gray-200 focus:border-yellowGreen-500 rounded-lg outline-none ring ring-transparent focus:ring-yellowGreen-500"
                type="text"
                placeholder="Cost Per Day"
                v-model="cost"
              />
            </div>
            <div class="w-full px-4 mb-4 flex items-center">
              <input
                type="checkbox"
                id="charge"
                v-model="initialCharge"
                class="w-5 h-5 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
              />
              <label for="charge" class="pl-4">Initial Charge</label>
            </div>
            <div class="w-full px-4 mb-4" v-if="initialCharge">
              <label class="block mb-1 text-md font-medium" for=""
                >Number of days</label
              >
              <input
                class="py-2 px-4 h-11 w-full text-gray-500 placeholder-gray-500 bg-gray-50 bg-opacity-40 border border-gray-200 focus:border-yellowGreen-500 rounded-lg outline-none ring ring-transparent focus:ring-yellowGreen-500"
                type="text"
                placeholder="Number of days"
                v-model="chargeDays"
              />
            </div>
          </div>
          <button
            class="flex items-center justify-center px-5 h-12 w-full mb-8 text-base font-semibold text-white bg-blue-600 hover:bg-blue-800 rounded-lg transition-all duration-300"
            type="button"
            @click="generateLink"
            v-if="type !== 'usdt'"
          >
            Create Subscription
          </button>

          <button
            class="flex items-center justify-center px-5 h-12 w-full mb-8 text-base font-semibold text-white bg-blue-600 hover:bg-blue-800 rounded-lg transition-all duration-300"
            type="button"
            @click="generateLinkUSD"
            v-if="type == 'usdt'"
          >
            Create Subscription
          </button>
        </form>
        <div v-if="link" class="w-full">
          <p class="text-center p-4">Subscription Generated</p>
          <textarea
            v-model="link"
            rows="5"
            class="textarea textarea-success w-full"
          ></textarea>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

function toHex(str) {
  var hex = "";
  for (var i = 0; i < str.length; i++) {
    hex += "" + str.charCodeAt(i).toString(16);
  }
  return hex;
}

async function encodeSubscription(
  _networkId,
  _boss,
  _token,
  _cost,
  _initdays = 0
) {
  var input_boss = _boss;
  var input_token = _token;

  var obj = JSON.stringify({
    network: _networkId,
    boss: input_boss,
    token: input_token,
    cost: _cost,
    initdays: _initdays,
  });

  var hash = toHex(obj) || null;

  return { hash: hash, link: "https://u.zpay.me/check/" + hash };
}

export default {
  data() {
    return {
      receiver: "0x000000000000000000000000000000000000dead",
      token: "0x000000000000000000000000000000000000dead",
      cost: 2,
      link: "",
      type: "usdt",
      types: [
        {
          name: "USDT",
          value: "usdt",
        },
        {
          name: "Token",
          value: "token",
        },
      ],
      initialCharge: false,
      chargeDays: 0,
      chain: "goerli",
      chainNames: {
        goerli: "11155111",
        bsc: "56",
        polygon: "137",
      },
    };
  },
  methods: {
    async generateLink() {
      const mec = this.receiver;
      const tok = this.token;

      if (mec && tok) {
        const subhash = await encodeSubscription(
          this.chainNames[this.chain],
          mec,
          tok,
          this.cost,
          this.chargeDays
        );

        this.link = subhash.link;
      } else {
        alert("Invalid Address");
      }
    },
    async generateLinkUSD() {
      const mec = this.receiver;

      this.link = `https://u.zpay.me/usd/${mec}/${this.cost}/${this.chargeDays}`;
    },
  },
};
</script>
