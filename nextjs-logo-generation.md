# Use this to generate Logos

```
import { ImageResponse } from "@vercel/og";
import { NextRequest } from "next/server";

export const runtime = "edge";

export async function GET(req: NextRequest) {
  const { searchParams } = new URL(req.url);
  const title = searchParams.get("title") || "Default Title";
  const subtitle =
    searchParams.get("subtitle") || "Custom image generation in Next.js 💥";

  // Fetch font from public directory
  const fontUrl = new URL("/fonts/heading.ttf", req.url).toString();
  const fontData = await fetch(fontUrl).then((res) => res.arrayBuffer());

  return new ImageResponse(
    (
      <div
        style={{
          height: "100%",
          width: "100%",
          display: "flex",
          flexDirection: "column",
          justifyContent: "center",
          alignItems: "center",
          background: "#ffd203",
          color: "white",
          fontFamily: "Inter",
          textAlign: "center",
          padding: "50px",
        }}
      >
        <h1 style={{ fontSize: 96, marginBottom: 20 }}>{title}</h1>
        {/* <p style={{ fontSize: 32, opacity: 0.8 }}>{subtitle}</p> */}
      </div>
    ),
    {
      width: 600,
      height: 600,
      fonts: [
        {
          name: "Inter",
          data: fontData,
          style: "normal",
        },
      ],
    },
  );
}

```
