<script lang="ts">
  import { Color } from "@nativescript/core";
  import { copyToClipboard } from "@nativescript/core/utils";

  let origin: string = "";
  let finalValue: string = "";

  const _voltearPalabra = (palabra: string) => {
    if (!palabra) return "";
    return palabra.split("").reverse().join("");
  };

  const formarFraseVolteada = (frase: string) => {
    if (!frase) return "";
    return frase
      .split(" ")
      .map((p) => (/[a-zA-Z0-9]+/.test(p) ? _voltearPalabra(p) : p))
      .join(" ");
  };

  const copyHandler = () => {
    copyToClipboard(finalValue);
    origin = "";
  };

  $: finalValue = formarFraseVolteada(origin);
</script>

<page>
  <actionBar title={formarFraseVolteada("🆚 Svelte")} />
  <stackLayout height="75%">
    <textField bind:text={origin} />
    <label textWrap="true">
      <formattedString>
        <span
          fontSize="25"
          textDecoration="underline"
          text={formarFraseVolteada("Alrevés :\n")}
        />
        <span
          fontSize="20"
          color={new Color("red")}
          fontWeight="bold"
          text="\t{finalValue}"
        />
      </formattedString>
    </label>
    <button text="Copy" on:tap={copyHandler} />
  </stackLayout>
</page>
