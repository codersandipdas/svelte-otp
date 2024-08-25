<script lang="ts">
  import OtpInput from '$lib/OtpInput.svelte';

  let otpValue = '';

  function handleOtpChange(newOtpValue: string) {
    otpValue = newOtpValue;
  }
</script>

<section
  class="h-screen flex flex-col gap-4 justify-center w-[400px] max-w-full mx-auto"
>
  <p class="text-left text-xl font-semibold text-black">Enter OTP</p>
  <p class="text-left text-base font-normal -mt-3 mb-2 text-black/50">
    Type or paste the OTP sent to you
  </p>
  <OtpInput
    length={6}
    inputType="number"
    placeholder="•"
    value={otpValue}
    onChange={handleOtpChange}
    inputClass="py-1 w-[40px]"
    containerClass="w-full overflow-hidden w-[400px]"
  />
  <div>
    <button class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-1.5 rounded"
      >Verify OTP</button
    >
  </div>
</section>
