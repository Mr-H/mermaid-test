# mermaid-test
Mermaid Diagram Test

```mermaid
---
config:
  theme: neo-dark
---
sequenceDiagram
  Actor Seller as Seller
  participant System as ProSale System
  participant AI_Module as AI Module
  Actor Buyer as Buyer
  participant AuctionBank as Auction Bank A/C
  participant SellerBank as Seller Bank A/C
  Actor Support as Support
  %% Seller setup
  Note right of Seller: Seller registration
  Seller ->> System: Register account
  System ->> Seller: Identity verification
  Note right of Seller: Seller login
  Seller ->> System: Login
  alt Successful Verification
    System ->> Seller: Access dashboard
    System ->> Seller: Display profile and analytics
  else Failed Verification
    System ->> Seller: Verification error 
    System ->> Seller: Return to Login
  end
  %% Seller item setup
  Note right of Seller: Item
  Seller ->> System: Fill out item listing
  Seller ->> System: Upload item image
  Seller ->> System: Set valuation or reserve price
  %% Have AI propose or improve the write up andn suggest a valuation 
  opt AI Module Interactions
    Note right of Seller: Invoke AI Module
    Seller ->> System: Launch item assist
    System ->> AI_Module: Verify and categorize item (Image Recognition)
    AI_Module ->> System: Analyze market and suggest prices
    System ->> Seller: Display AI suggestions
    alt Seller accepts suggestions
      Seller ->> System: Accept AI suggestions
    else Seller rejects suggestions
      Seller ->> System: Reject AI suggestions
    end
  end
  %% Review items and launch the auction 
  Note right of Seller: Review items and launch the auction
  Seller ->> System: Set auction details
  opt Review items
    Seller ->> System: Review & confirm items
  end
  System ->> Seller: Confirm auction setup
  Seller ->> System: Open the auction to buyers
  %% Shopping and bidding (the buyer doesn't need to be signed up or signed in to review the items but they do to bid)
  opt Buyer setup
    Note left of Buyer: Seller registration
    Buyer ->> System: Register account
    System ->> Buyer: Identity verification
  end
  Note left of Buyer: Shopping
  Buyer ->> System: Search items
  alt Successful Verification
    Note left of Buyer: Buyer login
    Buyer ->> System: Login
  else Failed Verification
    System ->> Buyer: Verification error
    System ->> Buyer: Return to login
  end
  loop 
    opt Update wishlist
      Buyer ->> System: Add/remove item to wishlist
    end
    Buyer ->> System: Place bid
    opt Seller updates
      System ->> Seller: Notify auction updates
    end
    System ->> Buyer: Notify when outbid
  end
  Note right of System: Auction Closed
  System ->> Buyer: Notify winning bidder
  %% Shipping or pickup
  Seller ->> System: Confirm shipping or pickup
  alt Shipping
    System ->> Seller: Coordinate logistics
    System ->> Buyer: Send shipping confirmation
  else Pickup
    System ->> Buyer: Confirm pickup details
  end
  %% Payment Processing
  Note left of Buyer: Buyer Payment Processing
  Buyer ->> System: Complete payment including shipping costs if applicable
  System ->> Buyer: Payment receipt
  System ->> System: Acknowledge payment receipt
  System ->> System: Deduct auction commission
  Note right of System: Seller Payment Settlement 
  System ->> AuctionBank: Deposit commission and shipping amount
  System ->> System: Confirm deposits
  System ->> Seller: Notify payment received
  System ->> Seller: Process payment to seller
  System ->> SellerBank: Deposit auction amount less commission and shippng 
  %% Post sales support 
  par Post sales support
    Buyer ->> System: Request support
    System ->> Support: Raise a ticket
    System ->> Buyer: Provide support ticket
  and  
    Seller ->> System: Request support
    System ->> Support: Raise a ticket
    System ->> Seller: Provide support ticket
  end
```
