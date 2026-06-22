from datetime import datetime

# =============================================================================
# DEMO MODE — No real API calls, no real credentials, no real data
# This script simulates exactly what the production version does,
# using fake data to demonstrate the report output and email format.
# =============================================================================

MOCK_NETWORKS = [
    {"id": "N_000000000001", "name": "Store #001 - New York"},
    {"id": "N_000000000002", "name": "Store #002 - Chicago"},
    {"id": "N_000000000003", "name": "Store #003 - Dallas"},
    {"id": "N_000000000004", "name": "Store #004 - Los Angeles"},
    {"id": "N_000000000005", "name": "Store #005 - Miami"},
]

MOCK_WHITELISTED_CLIENTS = [
    {"name": "POS-Terminal-1",      "mac": "aa:bb:cc:11:22:01", "network": "Store #001 - New York"},
    {"name": "POS-Terminal-2",      "mac": "aa:bb:cc:11:22:02", "network": "Store #001 - New York"},
    {"name": "BackOffice-PC",       "mac": "aa:bb:cc:11:22:03", "network": "Store #002 - Chicago"},
    {"name": "HP-Printer-Main",     "mac": "aa:bb:cc:11:22:04", "network": "Store #002 - Chicago"},
    {"name": "SecurityCamera-01",   "mac": "aa:bb:cc:11:22:05", "network": "Store #003 - Dallas"},
    {"name": "InventoryScanner-1",  "mac": "aa:bb:cc:11:22:06", "network": "Store #004 - Los Angeles"},
    {"name": "InventoryScanner-2",  "mac": "aa:bb:cc:11:22:07", "network": "Store #004 - Los Angeles"},
    {"name": "ManagerLaptop",       "mac": "aa:bb:cc:11:22:08", "network": "Store #005 - Miami"},
]

def simulate_api_calls():
    print("=" * 60)
    print("DEMO MODE — Simulating Meraki API calls")
    print("=" * 60)
    print(f"  [Simulated] GET /organizations/354602/networks")
    print(f"  [Simulated] Found {len(MOCK_NETWORKS)} networks")
    print()
    for network in MOCK_NETWORKS:
        clients = [c for c in MOCK_WHITELISTED_CLIENTS if c["network"] == network["name"]]
        print(f"  [Simulated] GET /networks/{network['id']}/policies/byClient")
        if clients:
            print(f"             Found {len(clients)} whitelisted client(s) in {network['name']}")
    print()

def build_html(whitelisted, run_date):
    rows = ""
    for i, c in enumerate(whitelisted, 1):
        rows += f"""
        <tr style="background-color: {'#f9f9f9' if i % 2 == 0 else 'white'};">
            <td style="padding:6px 12px;">{i}</td>
            <td style="padding:6px 12px;">{c['name']}</td>
            <td style="padding:6px 12px;">{c['mac']}</td>
            <td style="padding:6px 12px;">{c['network']}</td>
        </tr>"""

    return f"""
    <html>
    <body style="font-family: Arial, sans-serif; color: #333;">
        <h2 style="color: #1a73e8;">Weekly Whitelisted Clients Report</h2>
        <p><strong>Organization:</strong> The Cellular Connection, Inc.</p>
        <p><strong>Report Date:</strong> {run_date}</p>
        <p><strong>Total Whitelisted Clients:</strong> {len(whitelisted)}</p>
        <p style="background:#fff3cd; padding:8px; border-left:4px solid #ffc107;">
            <strong>DEMO MODE:</strong> This report uses simulated data.
            No real Meraki API calls were made.
        </p>
        <table><tr><th>#</th><th>Client Name</th><th>MAC Address</th><th>Network</th></tr></table>
        <br/>
        <p style="font-size:12px; color:#888;">
            This report was generated automatically via GitHub Actions (Demo Mode).
        </p>
    </body>
    </html>
    """

def print_email_preview(html, run_date):
    print("=" * 60)
    print("EMAIL PREVIEW (would be sent in production)")
    print("=" * 60)
    print(f"  To:      [recipients from EMAIL_TO secret]")
    print(f"  Subject: Weekly Whitelisted Clients Report — {run_date}")
    print(f"  Body:    HTML formatted table (see Actions log artifact)")
    print()
    print("HTML Report Preview (first 500 chars):")
    print("-" * 60)
    print(html[:500])
    print("...")
    print("-" * 60)

if __name__ == "__main__":
    run_date = datetime.utcnow().strftime("%B %d, %Y")
    print()
    print(f"Report Date: {run_date}")
    print()

    # Simulate the API scanning process
    simulate_api_calls()

    # Build the HTML report from mock data
    print("Building HTML report...")
    html = build_html(MOCK_WHITELISTED_CLIENTS, run_date)

    # Print summary
    print("=" * 60)
    print("REPORT SUMMARY")
    print("=" * 60)
    print(f"  Networks scanned:       {len(MOCK_NETWORKS)}")
    print(f"  Whitelisted clients:    {len(MOCK_WHITELISTED_CLIENTS)}")
    print()

    # Preview the email instead of sending it
    print_email_preview(html, run_date)

    print()
    print("Demo completed successfully.")
    print("In production, this report would be emailed to all recipients.")
