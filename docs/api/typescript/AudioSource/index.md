```ts
type AudioSource =
  | {
  type: "audioSourceBytes";
  bytes: Uint8Array;
}
  | {
  type: "audioSourceS3Location";
  location: S3Location;
};
```

Defined in: [src/types/media.ts:145](https://github.com/strands-agents/harness-sdk/blob/d1e1d0acbb3718d71741eceedee029cda695dcfd/strands-ts/src/types/media.ts#L145)

Source for an audio block (Class version).