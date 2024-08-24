# `@codersandip/svelte-otp`

A Svelte component for creating OTP (One-Time Password) inputs. This component allows for customizable OTP input length, supports different input types, and handles various user interactions such as input, paste, and backspace events.

## Screenshot

<img width="771" alt="Screenshot at Aug 24 20-17-52" src="https://github.com/user-attachments/assets/2d7a39d7-cf35-450b-b094-eeed9413db34">

## Features

- **Customizable OTP Input Length**: Set the number of OTP input fields.
- **Supports Different Input Types**: Choose between `text` and `number` input types.
- **Configurable Placeholder**: Set a custom placeholder for the input fields.
- **CSS Class Customization**: Apply custom CSS classes for styling.
- **Automatic Focus Management**: Automatically focuses the next input field as the user types.

## Installation

To install the package, use npm or yarn:

```bash
npm install @codersandip/svelte-otp
```

or

```bash
yarn add @codersandip/svelte-otp
```

## Usage

Import the OTP component into your Svelte application and use it as follows:

```svelte
<script>
  import {OtpInput} from '@codersandip/svelte-otp';

  let otpValue = '';

  function handleOtpChange(newOtpValue) {
    otpValue = newOtpValue;
  }
</script>

<OtpInput
  length={6}
  inputType="number"
  placeholder="•"
  value={otpValue}
  onChange={handleOtpChange}
  inputClass="custom-input-class"
  containerClass="custom-container-class"
/>
```

## Props

| Prop Name        | Type                   | Default    | Required | Description                                                              |
| ---------------- | ---------------------- | ---------- | -------- | ------------------------------------------------------------------------ |
| `length`         | number                 | `6`        | No       | The number of OTP input fields.                                          |
| `inputType`      | `"text"` \| `"number"` | `"number"` | No       | The type of input field. Possible values are `"text"` or `"number"`.     |
| `placeholder`    | string                 | `"•"`      | No       | The placeholder text for the input fields.                               |
| `value`          | string                 | `""`       | No       | The initial value of the OTP input fields.                               |
| `inputClass`     | string                 | `""`       | No       | Custom CSS class for the input fields.                                   |
| `containerClass` | string                 | `""`       | No       | Custom CSS class for the container.                                      |
| `onChange`       | function               | N/A        | Yes      | Callback function called with the current OTP value whenever it changes. |

## Styling

Customize the appearance of the OTP inputs using the provided CSS classes or by adding your own styles. For example:

```css
.custom-input-class {
  /* Custom styles for the input fields */
}

.custom-container-class {
  /* Custom styles for the container */
}
```

## Development

To build and test the package locally:

### Clone the Repository:

```bash
git clone https://github.com/codersandipdas/svelte-otp.git
cd svelte-otp
```

### Install Dependencies:

```bash
npm install
```

### Build the Package:

```bash
npm run build
```

### Link the Package Locally (for Testing):

```bash
npm link
```

### Use the Linked Package in Your Svelte Project:

```bash
npm link @codersandip/svelte-otp
```

## Contributing

Contributions are welcome! If you have suggestions or improvements, please open an issue or submit a pull request on [GitHub](https://github.com/codersandipdas/svelte-otp).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
