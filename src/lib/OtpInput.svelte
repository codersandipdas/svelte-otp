<script lang="ts">
  import { onMount } from 'svelte';

  export let length: number = 6;
  export let inputType: 'text' | 'number' | 'tel' | 'password' = 'number';
  export let placeholder: string = '•';
  export let value: string = '';
  export let inputWrapClass: string = '';
  export let inputClass: string = '';
  export let containerClass: string = '';
  export let onChange = (otpValue: string) => {};

  let otpValues: string[] = Array(length).fill('');
  let inputRefs: HTMLInputElement[] = [];

  onMount(() => {
    if (value && typeof value === 'string') {
      const initialValues = value.slice(0, length).split('');
      otpValues = [
        ...initialValues,
        ...Array(length - initialValues.length).fill(''),
      ];
    }
    updateOtpValue();
  });

  function handleInput(event: Event, index: number) {
    const input = event.target as HTMLInputElement;
    const inputValue = input.value;

    if (inputValue) {
      otpValues[index] = inputValue.slice(-1);

      if (index < length - 1) {
        inputRefs[index + 1]?.focus();
      }
    } else {
      otpValues[index] = '';
    }

    updateOtpValue();
  }

  function handleKeyDown(event: KeyboardEvent, index: number) {
    if (event.key === 'Backspace' && otpValues[index] === '' && index > 0) {
      inputRefs[index - 1]?.focus();
    }
  }

  function handlePaste(event: ClipboardEvent) {
    event.preventDefault();
    const pastedData = event.clipboardData?.getData('text');

    if (pastedData) {
      const pastedChars = pastedData.slice(0, length).split('');
      otpValues = [
        ...pastedChars,
        ...Array(length - pastedChars.length).fill(''),
      ];
      inputRefs[Math.min(pastedChars.length, length - 1)]?.focus();
      updateOtpValue();
    }
  }

  function updateOtpValue() {
    const otpValue = otpValues.join('');
    onChange(otpValue);
  }
</script>

<div class="otp-input-container {containerClass}">
  {#each otpValues as _, index}
    <div class="otp-input-wrap {inputWrapClass}">
      {#if inputType === 'number'}
        <input
          type="number"
          bind:this={inputRefs[index]}
          bind:value={otpValues[index]}
          on:input={(e) => handleInput(e, index)}
          on:keydown={(e) => handleKeyDown(e, index)}
          on:paste={handlePaste}
          maxlength="1"
          inputmode="numeric"
          autocomplete="one-time-code"
          class="otp-input {inputClass}"
          {placeholder}
        />
      {:else if inputType === 'password'}
        <input
          type="password"
          bind:this={inputRefs[index]}
          bind:value={otpValues[index]}
          on:input={(e) => handleInput(e, index)}
          on:keydown={(e) => handleKeyDown(e, index)}
          on:paste={handlePaste}
          maxlength="1"
          autocomplete="one-time-code"
          class="otp-input {inputClass}"
          {placeholder}
        />
      {:else if inputType === 'tel'}
        <input
          type="tel"
          bind:this={inputRefs[index]}
          bind:value={otpValues[index]}
          on:input={(e) => handleInput(e, index)}
          on:keydown={(e) => handleKeyDown(e, index)}
          on:paste={handlePaste}
          maxlength="1"
          autocomplete="one-time-code"
          class="otp-input {inputClass}"
          {placeholder}
        />
      {:else}
        <input
          type="text"
          bind:this={inputRefs[index]}
          bind:value={otpValues[index]}
          on:input={(e) => handleInput(e, index)}
          on:keydown={(e) => handleKeyDown(e, index)}
          on:paste={handlePaste}
          maxlength="1"
          autocomplete="one-time-code"
          class="otp-input {inputClass}"
          {placeholder}
        />
      {/if}
    </div>
  {/each}
</div>

<style>
  .otp-input-container * {
    box-sizing: border-box;
  }
  .otp-input-container {
    display: flex;
    gap: 8px;
    width: 100%;
  }

  .otp-input-wrap {
    flex: 1;
  }

  .otp-input {
    text-align: center;
    font-size: 18px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
  }

  .otp-input::placeholder {
    opacity: 0.4;
  }

  .otp-input:focus {
    outline: none;
    border-color: #007bff;
  }

  .otp-input::-webkit-outer-spin-button,
  .otp-input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  /* Firefox */
  .otp-input {
    -moz-appearance: textfield;
    appearance: textfield;
  }
</style>
